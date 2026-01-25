icon: simple/docker

## Build Docker Image
```
docker build -t <app> .
```

## View all docker images
```
docker images
```
```
docker image ls
```

## Run Docker Image
```
docker run <image name>
```

## Run in detached state
```
docker run -d <image name>
```

## Run with your specified name
```
docker run -d --name <unique name> <image name>
```

## View all docker containers 
```
docker ps -a
```

## View all running docker containers 
```
docker ps
```

## Remove single image
```
docker image remove <image-name>:<tag>
docker image rm <image-name>
docker image rm <id>
```

## Force remove running container
```
docker rm -f <container-id>
```

## Tag an Image
```
docker image tag <image-name>:<tag>
```

## Specific Guides

!!! Note "Cleaning up Images & Containers"

	### Clean dangling images
	```
    docker image prune
    ```
	
    ### Clean stopped containers
	```
    docker container prune
    ```


!!! Note "Pushing image to dockerhub"
	1. Get acess token from dockerhub website <br>
	2. Authenticate using <br>
        ```
		docker login -u NAME
        ```
	3. Enter Token <br>
	4. Tag the docker image to prepare for push
        ```
		docker image tag <image-name> <dockerhub-username>/<image-name>:<tag>
        ```
	5. Push image using <br>
       ```
       docker image push <dockerhub-username>/<image-name>:<tag>
       ```


!!! Note "Docker Volumes"
    ### Create docker volume
	```
    docker volume create <volume-name>
    ```

	### Inspect docker volume
	```
    docker volume inspect <volume-name>
    ```


!!! Note "Run docker with volume attached" 
    !!! Tip "Ensure $user has elevated privildeges to open folder"
	```
	docker run -d -p <host-port>:<container-port> -v path-data:/path/data <image-name>
    ```