## 🔨 Build & Images

# Build a Docker image from Dockerfile (current directory)
docker build .

# Build with a custom name and tag
docker build -t docker-ts:1 .

# List all Docker images
docker images

# Remove a specific image
docker rmi <image_id>

# Remove all unused (dangling) images
docker image prune

# Remove all unused images (including tagged)
docker image prune -a

# Rename / tag an image
docker image tag docker-ts:latest gowaliullah/ts-node-backend:v1


## 🐳 Containers

# Run a container and map ports
docker run -p 3000:3000 <image_id>

# Run a container with auto-remove when stopped
docker run -p 3000:3000 --rm <image_id>

# Run with a name
docker run -p 5000:5000 --rm --name docker-app <image_id>

# List running containers
docker ps

# List all containers (running + stopped)
docker ps -a

# Stop a container
docker container stop <container_id>

# Start a stopped container
docker container start <container_id>

# Start and attach logs
docker container start --attach <container_id>

# Remove container
docker rm <container_id>


## 📦 Volumes

# Run with named volume
docker run -p 5000:5000 --name ts-docker-container --rm \
  -v ts-docker-log:/app/logs ts-docker:v2

# Remove volume
docker volume rm ts-docker-log

# Run with bind mount
docker run -p 5000:5000 --name ts-docker-container --rm \
  -w /app \
  -v "$(pwd)":/app \
  -v /app/node_modules \
  -v ts-docker-log:/app/logs \
  ts-docker:v2

# Run with .env file
docker run -p 5000:5000 --name ts-docker-container --rm \
  --env-file .env \
  -w /app \
  -v "$(pwd)":/app \
  -v /app/node_modules \
  -v ts-docker-log:/app/logs \
  ts-docker:v2



## 🌐 Networking

# Create network
docker network create ts-docker-network

# List networks
docker network ls

# Inspect network
docker network inspect ts-docker-network

# Remove network
docker network rm ts-docker-network

# Example: run MongoDB in network
docker run --name mongodb --rm --network ts-docker-network mongo

# Example: run app container in same network
docker run -p 5000:5000 --name ts-docker-container --rm \
  --network ts-docker-network \
  --env-file .env \
  -w /app \
  -v "$(pwd)":/app \
  -v /app/node_modules \
  -v ts-docker-log:/app/logs \
  ts-docker:v2


## 🗄️ Databases (MongoDB Example)

# Run MongoDB with exposed port
docker run --name mongodb --rm -p 27017:27017 mongo

# Run MongoDB with volume + authentication
docker run --name mongodb --rm \
  -v ts-docker-db:/data/db \
  --network ts-docker-net \
  -e MONGO_INITDB_ROOT_USERNAME=ts-docker \
  -e MONGO_INITDB_ROOT_PASSWORD=ts-docker \
  mongo


## 💻 Multi-Container Setup

# Backend container
docker run --name ts-docker-backend --rm \
  --network ts-docker-net \
  --env-file .env \
  -w /app \
  -v "$(pwd)":/app \
  -v /app/node_modules \
  -v ts-docker-logs:/app/logs \
  -p 5000:5000 ts-docker-backend:v5

# Frontend container (with file watcher support)
docker run --name ts-docker-frontend --rm \
  -p 3000:3000 \
  --env-file .env.local \
  -w /app \
  -v "$(pwd)":/app \
  -v /app/node_modules \
  --network ts-docker-net \
  -e WATCHPACK_POLLING=true \
  ts-docker-frontend:v5

