# Routing mesh

It is a networking feature my docker that is responsible for distributing incoming packets of requests to the respective services handling these tasks. This process is known as `node balancing`. It sparns accross all the swarm nodes and does the balancing by listening on all the nodes for traffic to be able to distribute the tasks
