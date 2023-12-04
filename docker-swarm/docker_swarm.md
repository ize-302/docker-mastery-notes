# Docker swarm

A docker tool that allows us to deploy and mantain clusters of containers across many servers, instances or nodes.
Swarm is incactive on docker by default but can be activayed using the command `docker swarm init`
At the core of docker swarm we have the concept of manager and worker nodes;

## Manager and worker nodes

- A manager node is responsible for managing the cluster and orchestrating tasks. A manager node can have multiple workers
- Worker nodes are responsible for running the containers and executing the tasks assigned by the managers. Worker nodes do not participate in the management tasks. A worker node can have only one manager

A Docker Swarm can have multiple manager nodes for redundancy and fault tolerance. Having multiple managers allows the Swarm to continue functioning even if one or more manager nodes experience issues. It's recommended to have an odd number of manager nodes (e.g., 1, 3, 5) to ensure better fault tolerance in situations where a majority of managers need to agree on decisions.

## List out all nodes

```bash
docker node ls
```

## Creating a single node docker swarm service

Docker swarm makes use of `service` command to manage and scale containers. A service refers to a set of containers that are deployed and run across a cluster of Docker hosts. A worker node is made of one or more container known as replicas. replicas are copies of the same container. Its is very useful for scaling the application up or down

#### create a service

This creates a container based on alpine image.

```bash
docker service create alpine ping 8.8.8.8
```

#### list out services

```bash
docker service ls
```

#### list out tasks or containers in a service i.e worker node

```bash
docker service ps SERVICE_ID | SERVICE_NAME
```

### Update number of tasks of a service

```bash
docker service update SERVICE_ID | SERVICE_NAME --replicas INT_VALUE
# this adds two more tasks
```

### update a node's role from worker to manager. this should be ran in the manager instance

```bash
docker node update --role ROLE TARGET_NODE_HOSTNAME
# ROLE can be manager or worker
```

### Add a node as manager by default.

```bash
# First get token. shoukd be run in an existing manager instance
docker swarm join-token manager
# next. copy the output and run it in the node instance we want to upgrade to manager
```

Note: One great thing about container ochestration system, it is resposible for and ensures that all services specified are always running is a way that even if one or more of themm shuts down, they automatically get replaced within seconds. This is different from docker run where it is not able to automatically restart a container if there is a shutdown outcome or failure

![Docker swarm illustration](./illustrations/docker-swarm-illustration.png "Docker swarm illustration")

###

### Typical steps for orchestrating swarms

1. create vm instances
2. install docker on each instance by first shelling into an instance
3. initialize docker swarm with the command `docker swarm init` in one of the instant / node. This will initialize the current instance as a node, making it a manager and the leader by default
4. To make an instance join the swarm, copy the output from the previous run and paste in the new instance
   If you encounter any issue during setuo check [Docker swarm issues and fixes](./ps/docker_swarm_issues_fixes.md)
