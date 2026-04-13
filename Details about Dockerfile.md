
## এই Docker Compose File টা বুঝি 🐳

---

### এটা কী?

এটা একটা **`docker-compose.yml`** file — মানে Docker-কে বলছো **"কীভাবে আমার app চালাবে"** সেটার instruction।

---

### লাইন বাই লাইন বাংলায়

```yaml
version: '3'
```
> Docker Compose-এর **version 3** use করছি। এটা একটা format version।

---

```yaml
services:
  web:
```
> আমার একটা **service** আছে, তার নাম **`web`**। (একাধিক service থাকতে পারত, যেমন `web`, `db`, `redis` ইত্যাদি)

---

```yaml
    build:
      context: .
      dockerfile: Dockerfile.dev
```
> **Container কীভাবে build করবে:**
> - `context: .` → current folder থেকে build করো
> - `dockerfile: Dockerfile.dev` → `Dockerfile.dev` নামের file দিয়ে build করো (development এর জন্য আলাদা Dockerfile)

---

```yaml
    ports:
      - "3000:3000"
```
> **Port mapping** — বাম দিকটা তোমার **computer-এর port**, ডান দিকটা **container-এর port**
>
> মানে: তুমি browser-এ `localhost:3000` লিখলে → container-এর `3000` port-এ যাবে

---

```yaml
    volumes:
      - /app/node_modules
      - .:/app
```
> **Volumes** — এটা সবচেয়ে গুরুত্বপূর্ণ অংশ!
>
> - `.:/app` → তোমার **local folder**-এর সব file, container-এর `/app` folder-এ **sync** হবে। মানে তুমি code change করলে **সাথে সাথে** container-এও reflect করবে — restart লাগবে না! 🔥
>
> - `/app/node_modules` → container-এর `node_modules` যেন local folder দিয়ে **overwrite না হয়**। এটা container-এরটাই use করবে।

---

### পুরো ছবিটা এক নজরে

```
তোমার Computer
│
├── local code (./) ←──sync──→ container /app
│
└── localhost:3000 ←──port──→ container :3000
```

---

### Real Life উদাহরণ

> ভাবো তুমি একটা **React app** বানাচ্ছ।
> - Code লিখলে → automatically container-এ চলে যাবে ✅
> - Browser-এ `localhost:3000` দিলে → app দেখবে ✅
> - `node_modules` নিয়ে ঝামেলা নেই ✅

এটা মূলত **Development Environment** সেটআপের জন্য — তাই `Dockerfile.dev` use করছে।



<img width="1216" height="544" alt="image" src="https://github.com/user-attachments/assets/47b1c3c3-9ac0-43c8-a086-2baa3df2b38f" />
<img width="1227" height="578" alt="image" src="https://github.com/user-attachments/assets/62a196a1-149d-4a86-85dd-e46c54bc2c02" />
<img width="974" height="482" alt="image" src="https://github.com/user-attachments/assets/a06870be-9200-4cc5-8916-729f36b37104" />


<img width="1196" height="466" alt="image" src="https://github.com/user-attachments/assets/2953e0b8-f33d-4707-873f-acf7ba733372" />

<img width="659" height="508" alt="image" src="https://github.com/user-attachments/assets/67a95ed0-639d-4d6a-a696-85e40028ac89" />


```
FROM node:18-alpine

ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PWD=password

RUN mkdir -p /home/app

COPY . /home/app

# # set default dir so that next commands executes in /home/app dir
# WORKDIR /home/app

# will execute npm install in /home/app because of WORKDIR
#RUN npm install

# no need for /home/app/server.js because of WORKDIR
CMD ["node", "/home/app/server.js"]
```
