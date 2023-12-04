# Swarm stacks + production grade compose

It refers to a collection of services that are defined, configured and run together. Stack is usually represented by a docker compose file and consists of a set of instruction which describes the services, networks, volumes, secrets etc that makes up the application. Docker stacks simplifies the process of deploying and managing multi-service applications in a swarm cluster. It is simply a swarm compose file for production

#### Example of a stacks file

```yml
# docker-composeyml
version "3.9"

services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    networks:
      - webnet
    volumes:
      - nginx-conf:/etc/nginx/conf.d
    deploy:
      replicas: 2

  app:
    image: httpd:latest
    networks:
      - webnet
    volumes:
      - app-code:/usr/local/apache2/htdocs
    deploy:
      replicas: 2

  db:
    image: postgres:14
    secrets:
      - psql_user
      - psql_password
    environment:
      POSTGRES_PASSWORD: /run/secrets/psql_password
      POSTGRES_USER: /run/secrets/psql_user

networks:
  webnet:
    driver: overlay

volumes:
  nginx-conf:
    driver: local
  app-code:
    driver: local

secrets:
  psql_user:
    file: ./psql_user.txt
  psql_paswword:
    file: ./psql_paswword.txt
```

To deploy the above stack

```bash
docker stack deploy -c docker-compose.yml STACK_NAME
```

### storing secrets in swarm

There are multiple ways of storing secrets in swarm

```bash
echo 'SECRET' | docker secret create SECRET_NAME
```
