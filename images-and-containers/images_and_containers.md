# images vs containers

- An image is the binary files or source code of your application
- A container is the running process or running instance of an image

\*\*\* You can have have many container based off an image

## Example - running a container based off of nginx image

```bash
# nginx is the image
# "--publish | -p 80:80" opens a port 80 on the host ip and routes that traffic to the nginx container ip on port 80. You can use any port you want on the left as long as its not in use by anything else or another container
docker container run -p 80:80 nginx

# docker container run -p HOST_PORT:CONTAINER_PORT nginx
# in this case, port 80 on the host machine is mapped to port 80 inside the Nginx container.
```

open `localhost` in the browser to see

### Running in detached mode or in the background

```bash
docker container run -p 80:80 -d nginx
# OR
# docker container run --publish HOST_PORT:CONTAINER_PORT --detach nginx
```

### Custom-naming the container

```bash
docker container run -p 80:80 -d --name general-zod nginx
# i.e
# docker container run --publish HOST_PORT:CONTAINER_PORT --detach --name CUSTOM_NAME nginx
```

### List running containers

```bash
docker container ls
```

### List all containers; running or not

```bash
docker container ls -a
```

### List container logs

```bash
docker container logs CONTAINER_ID | CONTAINER_NAME
```

### Stopping the container

```bash
docker container stop CONTAINER_ID
```

#### Inspecting a host

```bash
docker container inspect CONTAINER_NAME_OR_ID
```

## What happens when we run a container?

- Looks for the image locally in the cache
- if found, uses that to instantiate a new container
- if not found, goes to remote image repository (defualts - dockerhub) to get it
- Downloads the latest version of that image
- Creates a new container based on the image and attempts to start
- assigns virtual ip to the container on a private netwok inside doccker engine
- opens up stated port on the host machine and forwards it to the stated port in container
- starts container using the CMD in the image dockerfile
