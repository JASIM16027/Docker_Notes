---

## Docker Pull এর পেছনে কী হয়?

Docker Hub থেকে image pull করা মানে শুধু একটা command চালানো না — এটা আসলে দুইটা component এর মধ্যে একটা **handoff**: **dockerd** পুরো process টা orchestrate করে, আর **containerd** actual কাজটা করে।

### দুইজন খেলোয়াড়

**dockerd** (Docker Daemon) হলো high-level interface। এটা incoming API requests handle করে, Docker Hub এর সাথে authentication করে, এবং networking ও volumes এর মতো বড় বিষয়গুলো দেখাশোনা করে।

**containerd** হলো dockerd এর নিচে কাজ করা industry-standard container runtime। এটা container এর পুরো lifecycle এর মালিক — image transfer, storage, এবং execution সব কিছু এর হাতে।

### `docker pull nginx:latest` চালালে কী হয়?

**Step 1 — CLI → dockerd:** Docker CLI একটা REST API request পাঠায় dockerd daemon এর কাছে।

**Step 2 — dockerd → Registry:** dockerd, Docker Hub এর সাথে যোগাযোগ করে image খোঁজে, credentials যাচাই করে, এবং download শুরু করে।

**Step 3 — dockerd → containerd:** Authentication শেষ হলে, dockerd actual fetch operation টা containerd এর হাতে তুলে দেয়।

**Step 4 — Content Management:** containerd image layers গুলো pull করে, একটা snapshotter filesystem এ unpack করে, এবং নিজের internal content store এ save করে রাখে।

### কে কী করে?

| কাজ | কে করে |
|---|---|
| API handling ও authentication | dockerd |
| Layer fetching ও storage | containerd |

সহজ কথায়: **dockerd দরজা খোলে, আর containerd সব কিছু ভেতরে নিয়ে যায়।**
