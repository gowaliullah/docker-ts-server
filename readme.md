# CMD for use docker


# Build a Docker image from the Dockerfile in the current directory
docker build .

# List all Docker images available on your system
docker images


# Run a container from an image and map port 3000 of container to port 3000 of host
docker run -p 3000:3000 <image_id>



# List all currently running containers
docker ps 


# Remove a running/stopped container by container ID
docker rm <container_id>


# Remove an image by image ID
docker rmi <image_id>


# List all containers (both running and stopped)
docker ps -a

# Remove a specific image
docker image rm <image_id>

# Remove a specific container
docker container rm <container_id>


# Remove all unused (dangling) images
docker image prune

# Start a stopped container
docker container start <container_id>

# Stop a running container
docker container stop <container_id>


# Run a container and automatically remove it when stopped (--rm flag)
docker run -p 3000:3000 --rm <image_id>


docker build -t docker-ts:1 .


docker run -p 5000:5000 --rm REPOSITORY:TAG


docker run -p 5000:5000 --rm --name docker-app REPOSITORY:TAG

docker image prune -a


# for create github repo
docker build -t gowaliullah/ts-node-backed:v1 .

# For rename
docker image tag docker-ts:lateat gowaliullah/ts-node-backed:v1

docker run -p 5000:5000 --name ts-docker-container --rm ts-docker:v1


docker run -p 5000:5000 --name ts-docker-container ts-docker:v1


docker container start attach ts-docker-container

docker container start --attach ts-docker-container


### Volumes
## Miror


 docker run -p 5000:5000 --name ts-docker-container --rm -v ts-docler-log:/app/logs ts-docker:v2

 docker volume rm ts-docler-log


## bind mound
docker run -p 5000:5000 --name ts-docker-container -v ts-docler-log://app/logs -w //app  -v "/home/waliullah/docker-with-typescript-backend/package.json
"://app -v //app/node_modules --rm  ts-docker:v2     

docker run -p 5000:5000 --name ts-docker-container -v ts-docler-log://app/logs -w //app  -v "//$(pwd)"://app -v //app/node_modules --rm  ts-docker:v2  

docker run -p 5000:5000 --name ts-docker-container -v ts-docler-log://app/logs -w //app  -v "//$(pwd)"://app -v //app/node_modules --rm --env-file ts-docker:v2  


## networking

docker network create ts-docker-network

docker network ls 

docker network inspect

docker network rm ts-docker-network

host.docker.internal instead of 172.17.0.2

<!-- container to container communicate -->
ip:172.17.0.2   
  
docker run --name mongodb --rm --network ts-docker-network mongo

docker run -p 5000:5000 --name ts-docker-container -v ts-docler-log://app/logs -w //app  -v "//$(pwd)"://app -v //app/node_modules --rm --env-file .env --network ts-docker-network ts-docker:v2  


docker

 docker pull mongo


 ## connecting with many container

 docker run --name mongodb --rm -p 27017:27017  mongo


 docker run --name ts-docker-backend-container --rm --network ts-docker-net --env-file .env -w //app -v ts-docker-logs://app/logs -v "//$(pwd)"://app -v //app/node_modules -p 5000:5000 ts-docker-backend:v5

# NextJS/React/Frontend Container
 docker run --name ts-docker-frontend-conatiner --rm -p 3000:3000 --env-file .env.local -w //app -v "//$(pwd)"://app -v //app/node_modules --network ts-docker-net -e WATCHPACK_POLLING=true ts-docker-frontend:v5