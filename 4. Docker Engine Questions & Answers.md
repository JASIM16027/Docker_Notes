
---

### 🐳 Docker Engine Questions & Answers

---

**Q1:** What is the primary function of the Docker Engine?
**A1:** Containers তৈরি করা এবং run করা। (Creating and running containers)

**Q2:** Which part of the host system does the Docker Engine use to operate?
**A2:** Host machine-এর kernel। (The host machine's kernel)

**Q3:** Name the three main internal components of the Docker Engine.
**A3:** dockerd, containerd, এবং runc। (dockerd, containerd, and runc)

**Q4:** What is the full name for the component abbreviated as 'dockerd'?
**A4:** Docker Daemon।

**Q5:** In the context of Docker internals, what is a 'Daemon'?
**A5:** একটি background process যা guardian এর মতো কাজ করে এবং silent ভাবে tasks perform করে। (A background process that acts as a guardian and performs tasks silently)

**Q6:** What are the three technical requirements for a process to be considered a 'Daemon'?
**A6:** Background process হতে হবে, requests শুনতে হবে, এবং অন্য processes-কে service দিতে হবে। (It must be a background process, listen for requests, and provide services to other processes)

**Q7:** How does a Daemon differ from a standard server process regarding terminal sessions?
**A7:** Daemon background এ চলে এবং terminal lock করে না। (A Daemon runs in the background and does not hold or lock the terminal session)

**Q8:** When does the Docker Daemon typically start running on a system?
**A8:** Computer boot হওয়ার সময় automatically start হয়। (It starts automatically when the computer boots up)

**Q9:** Which component of the Docker Engine is classified as the 'High-Level Container Runtime'?
**A9:** containerd

**Q10:** Which component of the Docker Engine is classified as the 'Low-Level Container Runtime'?
**A10:** runc

**Q11:** List the three primary management responsibilities of 'containerd'.
**A11:** Container lifecycle management, storage management, এবং image management।

**Q12:** What are the four core operational tasks performed by 'runc'?
**A12:** Container create করা, delete করা, stop করা, এবং clean করা। (Creating, deleting, stopping, and cleaning containers)

**Q13:** Which Linux kernel feature does 'runc' use to provide isolation for a container?
**A13:** Namespaces

**Q14:** Which Linux kernel feature does 'runc' use to set resource limits like CPU and RAM?
**A14:** Cgroups (Control Groups)

**Q15:** What happens to a Namespace in the kernel when 'runc' deletes a container?
**A15:** Namespace kernel থেকে delete হয়ে যায়।

**Q16:** Identify the two separate applications that are typically installed together in a Docker bundle.
**A16:** Docker Engine এবং Docker CLI

**Q17:** How does the Docker CLI communicate with the Docker Daemon?
**A17:** REST API request pathiye। (By sending REST API requests)

**Q18:** When a user runs 'docker version', which component receives the API request first?
**A18:** Docker Daemon (dockerd)

**Q19:** In the 'docker run' process, which component is responsible for pulling the image from a registry?
**A19:** Docker Daemon (dockerd)

**Q20:** Which component does 'dockerd' order to handle container-specific requests?
**A20:** containerd

**Q21:** Which component is directly responsible for interacting with the Linux Kernel to build a container?
**A21:** runc

**Q22:** How is the output of a running container delivered back to the user's terminal?
**A22:** Container → dockerd → CLI → user terminal

**Q23:** True or False: 'containerd' creates containers directly by communicating with the kernel.
**A23:** False

**Q24:** What specific hardware limits can be managed using Cgroups?
**A24:** CPU, RAM, network, এবং storage limits।

**Q25:** Docker Engine on Non-Linux Systems:
**A25:** Mac বা Windows এ Linux VM তৈরি করে kernel features access করার জন্য।

**Q26:** The component that provides the API interface for the Docker Daemon to communicate with the runtime is _____.
**A26:** containerd

**Q27:** The low-level runtime that implements the OCI specification to start containers is _____.
**A27:** runc

**Q28:** What does the Docker Daemon do immediately after receiving a 'create' request from the CLI?
**A28:** containerd কে order দেয় request handle করার জন্য।

**Q29:** What is the role of the Docker CLI in the Docker architecture?
**A29:** User command পাঠায় API requests হিসেবে server (Engine) কে।

**Q30:** Why is 'dockerd' considered a 'server'?
**A30:** Background এ চলে এবং incoming requests serve করে।

**Q31:** The ability of a daemon to perform tasks without notifying the user constantly is described as working _____.
**A31:** Invisibly বা silently

**Q32:** Which component is responsible for managing the actual file system and storage of containers?
**A32:** containerd

**Q33:** When 'runc' creates a container, what does it ask the kernel to create first?
**A33:** A new Namespace

**Q34:** Sequence Step: What follows the creation of a Namespace in the container creation process?
**A34:** Resource limits set করা using Cgroups

**Q35:** What is the primary difference between a standard background process and the Docker Daemon?
**A35:** Docker Daemon specifically server, listens & serves API requests

**Q36:** How are Docker CLI and Docker Engine related during installation?
**A36:** Separate software, একসাথে download & install হয়

**Q37:** Which component acts as the 'middleman' between the daemon and the low-level execution tool?
**A37:** containerd

**Q38:** In the 'hello-world' example, which component generates the actual text 'Hello from Docker'?
**A38:** Running container

**Q39:** Term: Control Groups (Cgroups)
**A39:** Linux kernel feature যা resource usage limit করে, account করে, এবং isolate করে।

**Q40:** Term: Namespaces
**A40:** Linux kernel feature যা system resources isolate & virtualize করে।

**Q41:** What is the specific role of 'runc' during the 'stop' command?
**A41:** Container process terminate করার signal handle করে।

**Q42:** Docker Daemon effectively manages the _____ of the entire container system.
**A42:** Orchestration or high-level flow

**Q43:** If 'dockerd' is stopped, can the Docker CLI still perform container operations?
**A43:** No, CLI daemon ছাড়া কাজ করতে পারে না।

**Q44:** Which component translates high-level container management into specific kernel instructions?
**A44:** runc

**Q45:** How does containerd interact with runc?
**A45:** runc কে call করে container create/manage করার জন্য।

**Q46:** What is the benefit of the 'daemon' architecture in Docker?
**A46:** Containers background এ persist করে terminal open না থাকলেও।

**Q47:** When a 'docker run' command is issued, which component verifies if the image exists locally?
**A47:** Docker Daemon (containerd image management এর মাধ্যমে)

**Q48:** What does 'High-Level' imply for 'containerd'?
**A48:** Abstract concepts like images, storage, container lifecycle manage করে।

**Q49:** What does 'Low-Level' imply for 'runc'?
**A49:** Direct OS features like Namespaces & Cgroups handle করে।

**Q50:** In the architecture, which component is the 'entry point' for all Docker requests?
**A50:** Docker Daemon (dockerd)

**Q51:** How does the Docker Daemon know what to do when you type a command?
**A51:** CLI command → REST API request → daemon understands

**Q52:** True or False: 'dockerd' is responsible for network interface limits.
**A52:** True, request initiate করে runc execution দিয়ে Cgroups use করে

**Q53:** The 'guardian' metaphor suggests 'dockerd' provides services to containers _____.
**A53:** Selflessly, user intervention ছাড়া

**Q54:** Which component would you check to find info about pulled container images?
**A54:** containerd

**Q55:** What is the final step in the container creation sequence before the container starts running code?
**A55:** Kernel isolated Namespace এবং resource Cgroups setup করে

---

If you want, I can also **turn this into a neat, colorful table or flashcard format** for **super easy revision**, Jasim.

Do you want me to do that next?
