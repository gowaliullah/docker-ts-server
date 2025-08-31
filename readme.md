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











