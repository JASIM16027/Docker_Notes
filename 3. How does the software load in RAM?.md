# How does the software load in RAM?


**Step 1 — Application Request**: User app-এ click করে, OS-এ request যায়।

**Step 2 — OS File System Check**: OS verify করে executable file disk-এ আছে কিনা। না থাকলে "File not found" error।

**Step 3 — Load from Disk**: OS disk থেকে app-এর executable code আর data small pages (4KB) আকারে RAM-এ তোলে। পুরোটা একসাথে না — demand paging-এ শুধু দরকারি অংশ আসে।

**Step 4 — Allocate Pages in RAM**: RAM-এ আলাদা আলাদা section তৈরি হয় — Code (.text), Data (.data), Heap (dynamic memory), Stack (function calls)। প্রতিটা section-এর জন্য specific pages allocate হয়।

**Step 5 — Shared Libraries**: অনেক app common libraries (graphics, networking) ব্যবহার করে। Library আগেই RAM-এ থাকলে reuse হয়, না থাকলে disk থেকে load করে link করে দেয়।

**Step 6 — PCB Create**: OS একটা Process Control Block বানায় যেখানে process-এর PID, state, memory locations, priority, resources সব track হয়। CPU scheduler এই PCB দেখে decide করে কোন process কখন চলবে।

**Step 7 — CPU Executes**: CPU RAM থেকে instructions fetch → decode → execute করে। যদি এমন কোনো page দরকার হয় যেটা RAM-এ নেই, **page fault** হয় আর OS disk থেকে সেটা এনে দেয়।

যেকোনো box-এ click করলে সেই step নিয়ে আরো detail জানতে পারবে!
