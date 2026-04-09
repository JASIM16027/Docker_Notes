# Docker Engine Internals

---

## 1. Docker Engine কি?

Docker Engine হলো core system যা containers build, run, আর manage করে।

- এটা একটামাত্র program নয় — এটা specialized components-এর collection।
- Host machine-এর kernel ব্যবহার করে lightweight ও isolated environment তৈরি করে।

**Analogy:**
Docker Engine = Factory
- `dockerd` → Factory Manager
- `containerd` → Assembly Line Supervisor
- `runc` → Floor Worker
- `Shim` → Babysitter

---

## 2. Core Components — 4টা

### dockerd (Docker Daemon) — Guardian

- Background process হিসেবে run করে
- CLI command শোনে REST API এর মাধ্যমে
- Images, containers, networks, volumes manage করে
- System boot এ auto-start হয়

**Daemon হওয়ার 3টি শর্ত:**
1. Background এ চলবে
2. Request listen করবে
3. Other processes কে service দেবে

> Memory trick: Silent parent — সবকিছু করছে, কিন্তু সামনে আসে না।

---

### containerd — High-Level Runtime (Manager)

- Container lifecycle manage করে: start, stop, delete
- Image ও storage handle করে
- Actual container creation runc কে delegate করে
- dockerd এর সাথে communicate করার জন্য API provide করে

> Memory trick: Project manager — plan করে, কিন্তু হাত দিয়ে কাজ করে না।

---

### runc — Low-Level Runtime (Worker)

- Kernel এর সাথে directly interact করে
- Container create, delete, stop, clean করে
- ব্যবহার করে:
  - **Namespaces** → container isolation
  - **Cgroups** → CPU, RAM, network, storage limit

> Memory trick: Engineer — manager এর instruction execute করে।

---

### Shim — Helper (Babysitter)

- Docker Daemon বা containerd crash হলেও container চলতে থাকে
- STDIN/STDOUT maintain করে
- Exit code containerd কে report করে

> Memory trick: Babysitter — parent চলে গেলেও বাচ্চা দেখে রাখে।

---

## 3. Docker CLI vs Docker Engine

| Aspect | Docker CLI (Client) | Docker Engine (Server) |
|--------|--------------------|-----------------------|
| Role | User interface | Container operations execute করে |
| Communication | REST API পাঠায় | Request receive করে ও process করে |
| Installation | Separate কিন্তু bundled | CLI এর সাথে একসাথে install হয় |
| Example | `docker run hello-world` | Image pull করে, container বানায়, run করায় |

**Flow:** CLI → REST API → dockerd

> Memory trick: CLI = Remote control | Engine = Machine doing actual work

---

## 4. Kernel Features — Namespace & Cgroups

### Namespaces → Isolation (আলাদা জগৎ)

- Container এর নিজস্ব private workspace তৈরি করে
- অন্য container বা host কে দেখতে পায় না
- Example: `/proc`, `/mnt`, `/net` আলাদা হয়ে যায়

> Memory trick: Namespace = Container-এর নিজের ঘর (private room)

---

### Cgroups → Resource Limits (সীমা নির্ধারণ)

- CPU, RAM, Network, Storage এর limit set করে
- Container host resource বেশি নিতে পারে না

> Memory trick: Cgroups = ঘরের size + furniture-এর সীমা

---

## 5. docker run hello-world — Step by Step Workflow

```
$ docker run hello-world
```

**Step 1:** User CLI তে command দেয়।

**Step 2:** CLI → command টাকে REST API request এ convert করে → dockerd কে পাঠায়।

**Step 3:** dockerd → request receive করে। Image locally আছে কিনা check করে। না থাকলে registry থেকে pull করে।

**Step 4:** dockerd → containerd কে request forward করে। containerd image ও storage prepare করে।

**Step 5:** containerd → runc কে instruct করে container create করতে।

**Step 6:** runc → kernel এ Namespace create করে (isolation দেওয়ার জন্য), তারপর Cgroups apply করে (resource limit set করার জন্য)। Container start হয়।

**Step 7:** Shim → container কে daemon থেকে independent রাখে। I/O handle করে, exit code track করে।

**Step 8:** Container output → dockerd → CLI → user terminal এ "Hello from Docker!" দেখায়।

**Full Flow:**
```
CLI → dockerd → containerd → runc → Kernel (Namespace + Cgroups) → Shim → Output back to CLI
```

---

## 6. Container Lifecycle — Start থেকে Delete

**Start করার সময়:**
1. runc → kernel কে Namespace create করতে বলে
2. Cgroup rules apply হয় (resource limit set হয়)
3. Container process start হয়

**Stop / Delete করার সময়:**
1. runc → process terminate করে, cleanup করে
2. Namespace kernel থেকে delete হয়
3. Resources release হয়

> Sequence memory hook: Isolation → Limit → Run → Stop → Cleanup

---

## 7. Image Management — কে কী করে

| Component | কাজ |
|-----------|-----|
| dockerd | Initial request handle করে, registry থেকে image pull করে |
| containerd | Image locally store করে ও manage করে |
| runc | Image handle করে না — শুধু container execute করে |

---

## 8. Key Truths — মনে রাখো

**ভুল ধারণা (False):**
- ✗ containerd সরাসরি container বানায় না — runc বানায়
- ✗ CLI একা কিছু করতে পারে না — dockerd লাগবেই
- ✗ runc image manage করে না

**সঠিক তথ্য (True):**
- ✓ dockerd stop হলে CLI কাজ করবে না
- ✓ Shim থাকলে daemon crash হলেও container চলতে থাকে
- ✓ Mac/Windows এ Docker একটি Linux VM use করে kernel access করতে
- ✓ Namespace = Isolation | Cgroups = Resource limit
- ✓ Image pull করে dockerd (via containerd)
- ✓ Output path: Container → dockerd → CLI → terminal

---

## 9. Architecture Advantage — কেন এই design?

- **High-Level vs Low-Level separation** → modular architecture
- **Daemon** → persistent, always running in background
- **Shim** → container independence from daemon
- **Kernel features** → lightweight isolation without full VM
- **Result:** Portable, isolated, resource-safe containers

---

## 10. Quick Revision — One Liners

| Term | মনে রাখো |
|------|---------|
| dockerd | Boss · Controller · Silent Guardian |
| containerd | Manager · High-level runtime |
| runc | Worker · Kernel executor |
| Shim | Babysitter · Keeps container alive |
| Namespace | Isolation · Container এর private room |
| Cgroups | Resource limits · Room size |
| CLI | Remote control · Client |
| Engine | Heavy lifter · Server |

---

## 11. Master Flow — মুখস্থ করো

```
User types command
       ↓
   Docker CLI
       ↓ (REST API request)
     dockerd       ← Boss, receives everything
       ↓
   containerd      ← Manager, prepares image & storage
       ↓
      runc         ← Worker, talks to kernel
       ↓
    Kernel         ← Creates Namespace + sets Cgroups
       ↓
   Container runs
       ↓
     Shim          ← Guards container independently
       ↓
  Output back to dockerd → CLI → User terminal
```

---

*Docker Engine = CLI + dockerd + containerd + runc + Shim + Kernel (Namespace + Cgroups)*
