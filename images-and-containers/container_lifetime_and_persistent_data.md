# Container lifetime and persistent data

Containers are meant to be immutable and disposable by design without fear of data loss. If there is any need to update the application or infrastructure, we can make these changes and just redeploy them on a new container.

### Persisting data

Containers are typically designed to be stateless, meaning that they don't retain data between runs. However, there are some situations where data might need to be preserved beyond a container's lifecycle e.g databases or some unique data, these are known as persistent data and docker gives us 2 ways of dealing with persistent data in a container

#### Volumes

This is a special location outside of the container's file system that we can persist data. When a container is deleted, it does not automatically remove its volume, the volume will have to be removed separately.

When spinning up a new container, it is adviced to add a custom volume name to it for easy recogniton. This is done using the `-v NAMED:VOLUME_PATH`. A good exampel is below:

```bash
docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -v mysql-db:/var/lib/mysql mysql
```

#### Bind mount

This is mapping the host file or directory to a container file or directory. so that the container can have access to the specified files or folder in the host direcotory and vice versa. Bind mounting cannot be run in the Docker file but rather during `docker container run ...`

Mapping a host directory to a container's file directory example

```bash
docker container run -d -p:80:80 --name nginx -v $(pwd):/usr/share/nginx/html nginx
```
