# Images

### What is an image?

An image is the application binaries and dependencies of an application and metadata on how to run it.

- Images are made up of layers of file changes and metadata
- Each layer has its own unique id and is stored only once on a host thereby saving storeage on the host and transfer time on push/pull

#### Check image history

```bash
docker image history IMAGE
```

#### Inspect an image

```bash
docker image inspect IMAGE
```

## Image tagging and pushing

This is similar to how github handles cloning or forking a repository whereby you can fork a repo, make it yours and push to github. Similarly, you can grab an already existing image and build your custom image off of that image, add a tag (defaults to latest if tag isnt specified) and push

### Image tagging using an already existing image

```bash
docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

### Pushing image to Dockerhub

```bash
docker image push TARGET_IMAGE[:TAG]
```

### Buiding images

```bash
docker image build -t IMAGE_NAME .
```

### Running container of the created image

```bash
docker container run -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
```
