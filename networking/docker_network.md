# Docker Network

## Defaults

- Each container is connected to a private virtual network known as "bridge network"
- Each virtual network routes via NET firewall on the host IP
- All containers on a virtual network can talk to eachother without assigning + opening port up
- Best pracice is to create a new virtual network for each app
  example:
  network my_web_app will have mysql and php/apache containers
  network my_api will have postgresql and nodejs containers

## Network CLI management

#### Creating a network

```bash
docker network create NETWORK_NAME
```

#### Listing existing networks

```bash
docker network ls
```

#### Connecting a host to an existing network

```bash
docker network connect NETWORK_NAME CONTAINER_NAME_OR_ID
```

#### Disconnecting a host from an existing network

```bash
docker network disconnect NETWORK_NAME CONTAINER_NAME_OR_ID
```

#### Inspect a network

```bash
docker network inspect NETWORK_NAME
```

## DNS and how containers talk to eachother

To enable multiple containers to be able to communicate with each other on the same docker host, the bridge network driver should be used. You should also ensure that the respective containers are connected to the same network

```bash
docker container exec -it CONTAINER_1 ping CONTAINER_2
```
