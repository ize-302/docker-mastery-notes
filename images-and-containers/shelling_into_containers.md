# Shelling into containers (without ssh)

Docker provides a way for us to get a shell terminal into containers

#### run a new container in interactive mode i.e using shell

```bash
docker container run -it --name CONTAINER_NAME IMAGE COMMAND
```

#### run command inside an already running container

```bash
docker container exec -it CONTAINER_NAME_OR_ID COMMAND
```

#### start up an existing but not running container in interactive mode

```bash
docker container start -ai CONTAINER_NAME_OR_ID
```
