---
title: Docker
description: This doc page covers tips and tricks you can use with docker.
icon: fontawesome/brands/docker
---

# Docker Tips and Tricks

### Building Docker Images
``` bash
# Regular standard/vanilla build
docker build -t {name-of-image} .

# Accounts for multi arch images
docker buildx build -t {name-of-image} .

# Build for specific platform(s)
docker build --platform=linux/arm64,linux/amd64 -t {name-of-image} .
```

### Running Docker Image
``` bash
# Run in non-detached state
docker run {image-name}

# Run in detached state
docker run -d {image-name}

# Run with your prefeered container name
docker run -d --name {unique name} {image-name}
```

### Managing Docker Images
``` bash
# View all docker images
docker images

# Remove a docker image via tag value
docker image remove {image-name}:{tag}

# Remove a docker image via image name
docker image rm {image-name}

# Remove a docker image via image id
docker image rm {id}

# Remove all un-used docker images at once
docker image rm $(docker images -q)

# Tag a docker image
docker tag {image-name}:{tag}

# Tag docker image for ECR
docker tag {image-name}:{tag} {account-id}.dkr.ecr.{region}.amazonaws.com/{image-name}:{tag}

# Tag docker image for dockerhub
docker tag {image-name}:{tag} {dockerhub-username}/{image-name}:{tag}

# Cleaning up dangling images
docker image prune


```

### Managing Docker Containers 
``` bash
# View runnning docker containers
docker ps

# View all docker containers (running and stopped)
docker ps -a

# Stop a running docker container
docker stop {container-id}

# Start a stopped docker container
docker start {container-id}

# Remove a stopped docker container
docker rm {container-id}

# Force remove a stopped/running docker container
docker rm -f {container-id}

# Cleaning up dangling containers
docker container prune
```

### Pushing Images to DockerHub
!!! Info "Key to know before pushing"
    Make sure to have an existing account created on dockerhub and you've geenrated a token from the website. <br> You can create an account here -> [DockerHub Sign Up](https://app.docker.com/signup) <br> You can learn how to generate token here -> [How to generate a token](https://docs.docker.com/security/access-tokens/)

``` bash linenums="1"
# Login to dockerhub
docker login --username {Your-Username}
Password: [paste your PAT here]

# Tag the docker image to prepare for push
docker image tag {image-name} {dockerhub-username}/{image-name}:{tag}

# Push image using {br}
docker image push {dockerhub-username}/{image-name}:{tag}

```

### Docker Volumes
``` bash
# Create a docker volume
docker volume create {volume-name}

# Inspect a docker volume
docker volume inspect {volume-name}
	
# Run docker container with volume attached
docker run -d -p {host-port}:{container-port} -v path-data:/path/data {image-name}
```
??? Tip "Docker Volumes Tips"
    Ensure `$user` has elevated privildeges to open local folder(s) when running
    a volume attached to a docker container. 


