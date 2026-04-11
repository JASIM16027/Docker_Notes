# docker-compose.yml
```
version: '3'

services:

  redis-server:
    image: 'redis'

  node-app:
    build: .
    ports:
      - "4001:8081"
```

---

```yaml
version: '3'
```
**Compose file-এর version।** Version 3 মানে Docker Compose-এর 3rd generation syntax ব্যবহার হচ্ছে। এটা সবচেয়ে common।

---

```yaml
services:
```
এখান থেকে **সব container-এর definition শুরু।** নিচে যা কিছু আছে সব এর ভেতরে।

---

```yaml
  redis-server:
    image: 'redis'
```
**প্রথম container — Redis।**
- নাম দেওয়া হয়েছে `redis-server`
- `image: 'redis'` মানে Docker Hub থেকে official Redis image নামিয়ে চালাবে
- কোনো `build` নেই, কারণ নিজে বানাতে হচ্ছে না — ready-made image ব্যবহার করছে

---

```yaml
  node-app:
    build: .
    ports:
      - "4001:8081"
```
**দ্বিতীয় container — তোমার Node.js app।**
- নাম `node-app`
- `build: .` মানে **current folder-এর `Dockerfile` দিয়ে** image বানাবে (নিজের code!)
- `ports: - "4001:8081"` মানে:
  - **বাইরে থেকে** `localhost:4001` এ access করলে
  - **container-এর ভেতরে** `8081` port-এ পৌঁছাবে

---

### Port mapping টা visual ভাবে বোঝো:

```
তুমি browser-এ টাইপ করো     container-এর ভেতরে
  localhost:4001      →→→       :8081 (app চলছে এখানে)
   [HOST PORT]                 [CONTAINER PORT]
```

---

### পুরো ছবিটা এক নজরে:

```
docker compose up চালালে...

┌─────────────────────────────────┐
│  redis-server (Redis)           │  ← image থেকে সরাসরি
│  redis:// redis-server:6379     │
└─────────────────────────────────┘
          ↕ (same network-এ কথা বলতে পারে)
┌─────────────────────────────────┐
│  node-app (তোমার code)         │  ← Dockerfile দিয়ে build
│  port 8081 → বাইরে 4001        │
└─────────────────────────────────┘
```

> **গুরুত্বপূর্ণ:** `redis-server` আর `node-app` automatically একই network-এ থাকে — তাই Node app থেকে Redis-এ connect করতে শুধু `redis-server` নামটা use করলেই হয়, কোনো IP লাগে না!


## Docker Compose Commands — সব এক জায়গায়

### 🚀 চালু করা
```bash
docker compose up              # সব service চালু (foreground)
docker compose up -d           # background-এ চালু (detached)
docker compose up --build      # image rebuild করে চালু
docker compose up -d --build   # rebuild + background (সবচেয়ে বেশি ব্যবহার)
```

---

### 🛑 বন্ধ করা
```bash
docker compose down            # সব বন্ধ + network remove
docker compose down -v         # সব বন্ধ + volume ও delete
docker compose stop            # বন্ধ করো, কিন্তু remove করো না
```

---

### 📋 Status দেখা
```bash
docker compose ps              # কোন container চলছে দেখো
docker compose logs            # সব service-এর logs
docker compose logs -f         # live logs (follow)
docker compose logs node-app   # শুধু একটা service-এর logs
```

---

### 🔁 Restart / Rebuild
```bash
docker compose restart              # সব restart
docker compose restart node-app     # শুধু একটা restart
docker compose build                # শুধু build, চালু না
docker compose build node-app       # একটা service build
```

---

### 🐚 Container-এর ভেতরে ঢোকা
```bash
docker compose exec node-app sh        # shell-এ ঢোকো
docker compose exec node-app bash      # bash-এ ঢোকো
docker compose exec redis-server redis-cli  # redis CLI
```

---

### 🗑️ Cleanup
```bash
docker compose down --rmi all     # image ও delete
docker compose down -v --rmi all  # সব কিছু clean
```

---

### তোমার project-এ সবচেয়ে বেশি কাজে লাগবে

| কাজ | Command |
|---|---|
| প্রথমবার চালু | `docker compose up -d --build` |
| Code change করলে | `docker compose up -d --build` |
| বন্ধ করতে | `docker compose down` |
| Log দেখতে | `docker compose logs -f` |
| Status চেক | `docker compose ps` |


## Docker Container Status Codes

| Code | মানে |
|---|---|
| **0** | We exited and everything is OK |
| **1, 2, 3, etc** | We exited because something went wrong! |

---

### সহজ ভাষায়

**Exit Code 0 — সব ঠিকঠাক ✅**
- Container নিজে থেকে **সফলভাবে** কাজ শেষ করে বন্ধ হয়েছে
- কোনো error নেই
- যেমন: `docker compose down` করলে সব container `0` দিয়ে বন্ধ হয়

**Exit Code 1, 2, 3... — কিছু একটা ভুল হয়েছে ❌**
- Container **crash** করেছে বা error-এ পড়েছে
- যেমন:
  - `1` → General error (code-এ bug, file not found)
  - `2` → Misuse of command
  - `137` → Container-কে force kill করা হয়েছে (OOM বা `kill -9`)

---

### কীভাবে দেখবে?

```bash
docker compose ps          # STATUS column দেখো

docker inspect <container> --format='{{.State.ExitCode}}'
```

---

### Real life example

```
NAME         STATUS
node-app     Exited (0)    ✅ ঠিকমতো বন্ধ হয়েছে
node-app     Exited (1)    ❌ কিছু একটা ভুল — logs দেখো!
```

> যদি `Exited (1)` দেখো — সাথে সাথে `docker compose logs node-app` চালাও, কারণটা ওখানেই লেখা থাকবে।



## Docker Restart Policies

Container crash করলে বা বন্ধ হলে Docker কী করবে — সেটাই Restart Policy।

---

### ৪টা Policy

**`"no"` — কিছুই করবে না ❌**
- Container বন্ধ হলে বা crash করলে — Docker চুপ করে বসে থাকবে
- আর চালু করবে না
- এটাই **default** — yml-এ কিছু না লিখলে এটাই হয়
- কখন ব্যবহার: Development-এ, যখন manually control করতে চাও

---

**`always` — সবসময় restart করবে ♾️**
- যেকোনো কারণে বন্ধ হোক — আবার চালু হবে
- এমনকি তুমি `docker compose stop` করলেও — Docker daemon restart হলে আবার উঠবে
- কখন ব্যবহার: Web server, Database — যেগুলো সবসময় চালু থাকা দরকার

---

**`on-failure` — শুধু error হলে restart করবে ⚠️**
- Exit code `0` হলে → restart করবে না (সফলভাবে বন্ধ হয়েছে)
- Exit code `1, 2, 3...` হলে → restart করবে (কিছু ভুল হয়েছে)
- কখন ব্যবহার: Worker/Job যেটা নিজে থেকে শেষ হতে পারে, কিন্তু crash করলে উঠতে হবে

---

**`unless-stopped` — তুমি না থামানো পর্যন্ত চলবে 🔒**
- `always`-এর মতোই, কিন্তু একটা পার্থক্য:
- তুমি manually `docker compose stop` করলে → আর উঠবে না
- `always` হলে Docker restart হলেও উঠে, `unless-stopped` হলে উঠে না যদি তুমি থামিয়ে রাখো
- কখন ব্যবহার: Production server — তুমি ইচ্ছা করে বন্ধ করলে বন্ধই থাকুক

---

### `always` vs `unless-stopped` পার্থক্য

| পরিস্থিতি | `always` | `unless-stopped` |
|---|---|---|
| Container crash করলে | ✅ restart | ✅ restart |
| তুমি `stop` করলে, তারপর server reboot | ✅ উঠবে | ❌ উঠবে না |

---

### yml-এ কীভাবে লিখবে

```yaml
services:
  redis-server:
    image: 'redis'
    restart: always        # ← এখানে লেখো

  node-app:
    build: .
    restart: on-failure
    ports:
      - "4001:8081"
```

---

### কোনটা কখন বেছে নেবে?

| Situation | Policy |
|---|---|
| Local development | `no` (default) |
| Production web server | `always` |
| Background job/worker | `on-failure` |
| Production, manual control চাই | `unless-stopped` |
