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



# Docker Compose — বিস্তারিত গাইড

## Multi-Container Apps কী?

বাস্তব জীবনে একটা অ্যাপ সাধারণত একাধিক সার্ভিস নিয়ে তৈরি হয়। যেমন একটা ওয়েব অ্যাপে থাকে:

- **Frontend** (React/HTML)
- **Backend** (Node.js/Python)
- **Database** (PostgreSQL/MySQL)
- **Cache** (Redis)

এই সবগুলো আলাদা আলাদা container এ চলে। Docker Compose দিয়ে এগুলো একসাথে manage করা যায় — একটাই `docker-compose.yml` ফাইলে সব define করো, তারপর একটাই command এ সব চালু হয়।

---

## docker-compose.yml এর মূল গঠন

```yaml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/mydb
    depends_on:
      - db
      - redis

  db:
    image: postgres:15
    volumes:
      - db_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=mydb

  redis:
    image: redis:alpine

volumes:
  db_data:
```

এখন এই ফাইলটা রান করতে:
```bash
docker-compose up        # সব container চালু
docker-compose up -d     # background এ চালু
docker-compose down      # সব বন্ধ
```

---

## ১. Multi-Container — Services কীভাবে কথা বলে?

Container গুলো একে অপরকে **service name** দিয়ে চেনে। যেমন backend থেকে database connect করতে `localhost` লেখা যাবে না — লিখতে হবে `db` (service এর নাম)।

```python
# backend কোডে এভাবে database connect করবে
DATABASE_URL = "postgres://user:pass@db:5432/mydb"
#                                        ^^
#                              এটা container এর service name
```

`depends_on` দিয়ে বলা যায় কোন service আগে চালু হবে:

```yaml
backend:
  depends_on:
    - db      # db চালু না হলে backend চালু হবে না
    - redis
```

---

## ২. Volumes — ডেটা কোথায় থাকে?

Container বন্ধ করলে ভেতরের সব ডেটা মুছে যায়। Volumes দিয়ে ডেটা টিকিয়ে রাখা যায়।

### দুই ধরনের Volume আছে:

**Named Volume** — Docker নিজে manage করে, সবচেয়ে সহজ:

```yaml
services:
  db:
    image: postgres:15
    volumes:
      - db_data:/var/lib/postgresql/data
      # db_data = volume এর নাম
      # /var/lib/postgresql/data = container এর ভেতরে যেখানে data থাকে

volumes:
  db_data:   # এখানে declare করতে হবে
```

**Bind Mount** — তোমার computer এর folder সরাসরি container এ দেখাবে। Development এ খুব কাজে লাগে:

```yaml
services:
  backend:
    volumes:
      - ./backend:/app
      # ./backend = তোমার PC তে folder
      # /app = container এর ভেতরে folder
```

এটার মানে হলো — তুমি `./backend` ফোল্ডারে কোড edit করলে সাথে সাথে container এর ভেতরেও বদলে যাবে। Hot reload কাজ করবে!

### Volume commands:
```bash
docker volume ls           # সব volume দেখো
docker volume inspect db_data   # volume এর details দেখো
docker volume rm db_data   # volume মুছো
```

---

## ৩. Networks — Container গুলো কীভাবে যুক্ত?

Docker Compose automatically একটা **default network** বানায়। সব service সেই network এ থাকে, তাই তারা একে অপরকে service name দিয়ে চিনতে পারে।

তবে চাইলে নিজে network বানানো যায়:

```yaml
services:
  backend:
    networks:
      - app_network
      - db_network

  db:
    networks:
      - db_network   # শুধু db_network এ আছে

  frontend:
    networks:
      - app_network  # শুধু app_network এ আছে

networks:
  app_network:
  db_network:
```

এখানে frontend সরাসরি db কে access করতে **পারবে না** কারণ তারা আলাদা network এ। শুধু backend পারবে — এটাই security best practice।

---

## ৪. Environment Variables — Secret জিনিস কোথায় রাখবে?

Database password, API key — এগুলো সরাসরি কোডে লেখা যাবে না। Environment variable ব্যবহার করতে হয়।

### পদ্ধতি ১ — সরাসরি compose file এ লেখা (ছোট project এ চলে):

```yaml
services:
  backend:
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/mydb
      - JWT_SECRET=mysecretkey
      - PORT=5000
```

### পদ্ধতি ২ — `.env` ফাইল থেকে নেওয়া (সঠিক পদ্ধতি):

`.env` ফাইল বানাও:
```
DATABASE_URL=postgres://user:pass@db:5432/mydb
JWT_SECRET=mysecretkey123
PORT=5000
```

`docker-compose.yml` এ:
```yaml
services:
  backend:
    env_file:
      - .env    # .env ফাইল থেকে সব variable নেবে
```

অথবা নির্দিষ্ট variable বেছে নেওয়া:
```yaml
services:
  backend:
    environment:
      - DATABASE_URL=${DATABASE_URL}   # .env থেকে নেবে
      - PORT=${PORT}
```

> ⚠️ `.env` ফাইল কখনো GitHub এ push করবে না। `.gitignore` এ add করো।

---

## সম্পূর্ণ উদাহরণ — Node.js + PostgreSQL + Redis

```yaml
version: '3.8'

services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      - ./frontend:/app        # hot reload এর জন্য
    networks:
      - app_network

  backend:
    build: ./backend
    ports:
      - "5000:5000"
    volumes:
      - ./backend:/app         # hot reload এর জন্য
    env_file:
      - .env
    depends_on:
      - db
      - redis
    networks:
      - app_network
      - db_network

  db:
    image: postgres:15
    volumes:
      - db_data:/var/lib/postgresql/data   # data টিকিয়ে রাখার জন্য
    environment:
      - POSTGRES_USER=${DB_USER}
      - POSTGRES_PASSWORD=${DB_PASS}
      - POSTGRES_DB=${DB_NAME}
    networks:
      - db_network

  redis:
    image: redis:alpine
    volumes:
      - redis_data:/data
    networks:
      - db_network

volumes:
  db_data:
  redis_data:

networks:
  app_network:
  db_network:
```

---

## Quick Command চিটশিট

```bash
docker-compose up -d              # সব চালু করো (background)
docker-compose down               # সব বন্ধ করো
docker-compose down -v            # বন্ধ + volumes মুছো
docker-compose logs backend       # backend এর logs দেখো
docker-compose exec backend bash  # backend container এ ঢোকো
docker-compose ps                 # কোন container চলছে দেখো
docker-compose build              # image rebuild করো
```

---

সহজ করে মনে রাখো — **services** মানে কোন কোন container চলবে, **volumes** মানে ডেটা কোথায় সেভ হবে, **networks** মানে কে কার সাথে কথা বলতে পারবে, আর **environment variables** মানে secret জিনিসপত্র কোথায় রাখবে।
