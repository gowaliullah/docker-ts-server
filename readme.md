# CMD for use docker


# Build a Docker image from the Dockerfile in the current directory
docker build .

# List all Docker images available on your system
docker images


# Run a container from an image and map port 3000 of container to port 3000 of host
docker run -p 3000:3000 <image_id>