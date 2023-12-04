# Secrets with services

Easiest and secured solution for storing secrets in swarm. Secrets is a built-in feature in swarm and does not require any extra installation.

Secrets are first created like this:

```bash
# create secret from an existing file.
docker secret create SECRET_NAME SECRET_FILE.EXT
#Say you have an existing pg_psswrd.txt file with 'mydbpassword' as its content
# SECRET_NAME could be anything, its just for identification purpose. So if I chose to use a name it would be:
docker secret create pg_psswrd pg_psswrd.txt
# OR

# via command line on the fly
printf 'SECRET' | docker secret create SECRET_NAME -
# the '-' on the end is telling the cli to read from the standard input i.e what was printed
printf 'user' | docker secret create pg_usr -
```

Then the secret is assugned to a service. Only containers in assigned service can see them. Secrets look like files in container but are actualy in-memory file system

```bash
/run/secrets/SECRET_NAME
# OR
/run/secrets/SECRET_ALIAS
```

For local development, docker-compose can use file-based secrets (but not secure) but it allows us to use secrets in local machine.

### List out secrets that have been created

```bash
docker secret ls
```

### Attaching secret to a service

```bash
docker service create --name pgdb --secret pg_psswrd --secret pg_usr -e POSTGRES_PASSWORD_FILE=/run/secrets/pg_psswrd -e POSTGRES_USER_FILE=/run/secrets/pg_usr postgres:14
```

### See secrets attached to a running container

Make sure you are in the node in which the container exists. Run `docker container ls` to verify

```bash
# Make sure you are in the node in which the container exists
docker container ls

#SSH into the container
docker container exec -it CONTAINER_NAME sh

## list out secrets in the current running process
cd /run/secrets && ls

## check value of a secret
cat /run/secrets/SECRET_NAME
```

More: https://docs.docker.com/engine/swarm/secrets/
