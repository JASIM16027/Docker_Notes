This command breaks down as:

```bash
docker compose -f 'docker-compose.yml' up -d --build
```

| Flag | Meaning |
|---|---|
| `-f 'docker-compose.yml'` | Explicitly specify the compose file to use |
| `up` | Create and start all containers |
| `-d` | Detached mode — runs in background |
| `--build` | Force rebuild images before starting |

---

### Common variations

```bash
# Rebuild and start a specific service only
docker compose -f 'docker-compose.yml' up -d --build api

# Scale while starting
docker compose -f 'docker-compose.yml' up -d --build --scale api=3 --scale worker=2

# Force recreate containers even if nothing changed
docker compose -f 'docker-compose.yml' up -d --build --force-recreate

# Remove orphan containers (from removed services)
docker compose -f 'docker-compose.yml' up -d --build --remove-orphans
```

---

### Useful follow-up commands

```bash
# Watch live logs for all services
docker compose -f 'docker-compose.yml' logs -f

# Logs for a specific service
docker compose -f 'docker-compose.yml' logs -f api

# Check running containers and their status
docker compose -f 'docker-compose.yml' ps

# Stop everything
docker compose -f 'docker-compose.yml' down

# Stop and remove volumes (wipes DB data)
docker compose -f 'docker-compose.yml' down -v
```

---

### Typical dev workflow

```bash
# 1. Start everything fresh
docker compose -f 'docker-compose.yml' up -d --build --remove-orphans

# 2. Monitor logs
docker compose -f 'docker-compose.yml' logs -f

# 3. Make code changes (volumes handle hot reload)

# 4. Rebuild only changed service
docker compose -f 'docker-compose.yml' up -d --build api

# 5. Tear down
docker compose -f 'docker-compose.yml' down
```

> 💡 If your file is simply named `docker-compose.yml`, the `-f` flag is optional — Docker Compose picks it up automatically. It's useful when you have multiple files like `docker-compose.prod.yml` or `docker-compose.test.yml`.

```yml
# version: '3'
# services:
#   mongodb: #mongodb container name
#     image: mongo 
#     ports:
#       - 27017:27017 # host machine port: container port 
#     environment:
#       - MONGO_INITDB_ROOT_USERNAME=admin
#       - MONGO_INITDB_ROOT_PASSWORD=password
#     volumes:
#       - mongo-data:/data/db
#   mongo-express: #mongodb container name
#     image: mongo-express 
#     restart: always
#     ports:
#       - 8081:8081  # host machine port: container port 
#     environment:
#       - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
#       - ME_CONFIG_MONGODB_ADMINPASSWORD=password
#       - ME_CONFIG_MONGODB_SERVER=kubernetes-mongodb-1
# volumes:
#   mongo-data:
#     driver: local


version: '3.8'

services:
  mongodb:
    image: mongo
    container_name: mongodb
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    ports:
      - "27017:27017"
    networks:
      - mongo-network

  mongo-express:
    image: mongo-express
    container_name: mongo-express
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: password
      ME_CONFIG_MONGODB_SERVER: mongodb
    ports:
      - "8081:8081"
    networks:
      - mongo-network

networks:
  mongo-network:
    driver: bridge
```
