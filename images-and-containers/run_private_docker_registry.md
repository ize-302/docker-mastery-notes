# Run a private docker registry

```bash
# run the private registry image
docker container run -d -p 5000:5000 --name registry registry
# OR using volume
docker container run -d -p 5000:5000 --name registry -v $(pwd)/registry-data:/var/lib/registry registry
# if regsitry is created using volume, you can check whats in the volume using this command:
ls -lG registry-data/


# tag an image
docker tag IMAGE 127.0.0.1:5000/IMAGE
# e.g
docker tag hello-world 127.0.0.1:5000/hello-world

# Push newly tagged image to private image registry
docker image push 127.0.0.1:5000/IMAGE

# To confirm that the newly tagged image exists in prvate registry, remove the tagged image from local image cache
docker image rm 127.0.0.1:5000/IMAGE
# and pull from new private registry. This pulls from the private registry called `registry` created at the beginning
docker image pull 127.0.0.1:5000/IMAGE
```

#### Note

[Securing docker registry with TLS and authentication](https://training.play-with-docker.com/linux-registry-part2/)

### Run a private docker registry with swarm

Works same way with container except that it uses `services create` instead of `container run`

```bash
docker service create -d -p 5000:5000 --name registry registry
# OR using volume
docker service create -d -p 5000:5000 --name registry -v $(pwd)/registry-data:/var/lib/registry registry
```

Note: All nodes will have access to the newly created registry i.e they can see `127.0.0.1:5000`
