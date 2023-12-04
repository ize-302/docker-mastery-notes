1. If you encounter this error when attempting to initialize docker swarm:

```bash
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/swarm/init": dial unix /var/run/docker.sock: connect: permission denied
```

The error message you're encountering indicates a permission issue with the Docker daemon socket. The Docker daemon socket is the communication endpoint that Docker clients (like the docker command-line interface) use to communicate with the Docker daemon. Run the following command

```bash
sudo chmod 666 /var/run/docker.sock # modify file perimission
OR
# sudo usermod -aG docker $USER # adding the user to the `docker` user group
```
