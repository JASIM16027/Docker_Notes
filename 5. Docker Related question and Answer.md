

## 🖥️ OS — Process & User Space

**Q: Application processes কোথায় execute হয়?**
→ User Space (User Mode) এ — directly hardware access safe না।

**Q: CPU, RAM, Disk তে directly কার access আছে?**
→ শুধু **Kernel** এর।

**Q: App hardware দরকার হলে কী করে?**
→ **System Call** করে Kernel কে request পাঠায়।

**Q: App binary কোথায় থাকে (not running)?**
→ **Hard Disk** এ।

**Q: Double-click করলে কী হয়?**
→ Binary **RAM এ load** হয় → User Space এ running process হয়।

**Q: Go 1.16 আর 1.25 একসাথে কঠিন কেন?**
→ OS একটা system path এ শুধু **একটা version** রাখতে দেয়।

**Q: Go overwrite হলে Spotify কী হবে?**
→ Spotify crash করবে — required version খুঁজে পাবে না।

---

## 🌐 Namespaces

**Q: Namespace কী করে?**
→ Process কে isolated environment দেয় — file system, network, PID সব আলাদা।

**Q: Linux start এ সব app কোন Namespace এ?**
→ **Initial Namespace** এ।

**Q: Namespace কী তৈরি করে?**
→ আলাদা **"World"** — process মনে করে সে একাই আছে।

**Q: Process Namespace কীভাবে চেনে?**
→ OS তাকে Namespace ID দেয় এবং শুধু allocated storage দেখায়।

**Q: Spotify NodeJS এর file কেন দেখতে পায় না?**
→ **Namespace isolation** — আলাদা Namespace এ থাকলে একটা আরেকটার file দেখে না।

**Q: নতুন Namespace এ assign হলে process কী দেখে?**
→ শুধু সেই Namespace এর files, network, আর process।

---

## ⚙️ C-Groups (Control Groups)

**Q: C-Groups কী control করে?**
→ Resource limits — **CPU, RAM, Disk I/O** কতটুকু use করা যাবে।

**Q: Namespaces vs C-Groups?**
→ Namespaces = কী দেখবে (visibility) | C-Groups = কতটুকু পাবে (limits)

**Q: 500MB Disk I/O limit করতে কী ব্যবহার?**
→ **C-Groups**

**Q: 1 Mbps network limit কোনটা দিয়ে?**
→ **C-Groups**

---

## 📦 Containers & Container Images

**Q: Container কী?**
→ Namespaces + C-Groups দিয়ে তৈরি isolated Linux environment। "Frog in a Well" — ব্যাঙ মনে করে কূপই সারা পৃথিবী।

**Q: Container এর নিজের Kernel আছে?**
→ না — host machine এর Kernel share করে।

**Q: Container কেন "Virtual Computer"?**
→ নিজস্ব virtual RAM, CPU limits, file system আছে — independent machine এর মতো।

**Q: Container Image কী?**
→ Container এর **static snapshot** — একটা নির্দিষ্ট মুহূর্তের "screenshot"।

**Q: Image vs Container পার্থক্য?**
→ Image = stopped & static | Container = active & running

**Q: একটা Image থেকে কতটা Container?**
→ **Unlimited** — হাজার হাজার identical container বানানো যায়।

**Q: Image share করার সুবিধা?**
→ Colleague ঠিক same environment পাবে — same dependencies, same files।

**Q: Container নিজের hard disk ব্যবহার করে?**
→ না — host এর disk share করে, Namespaces দিয়ে isolated area তে restrict।

**Q: Multiple container এ Kernel reuse হয়?**
→ হ্যাঁ — সবাই host এর একই Kernel share করে।

**Q: Container এ process কি জানে Kernel share হচ্ছে?**
→ না — মনে করে নিজের dedicated Kernel & hardware আছে।

**Q: Container A কি Container B এর process দেখতে পারে?**
→ না — **Namespaces** এদের Process Tree isolate করে রাখে।
