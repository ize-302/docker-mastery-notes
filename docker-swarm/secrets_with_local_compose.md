# Secrets with local docker compose

Docker compose provides a way to use secrets in out local dev environment. Although this does not work with the `external` method but only with file based secrets i.e storing the secrets in files

```yml
# docker-compose.yml
# version should be atleast 3.1
version: "3.9"

services:
  pgdb:
    image: postgres:14
    secrets:
      - pg_usr
      - pg_psswrd
    environment:
      - POSTGRES_PASSWORD_FILE=/run/secrets/pg_pssword
      - POSTGRES_USER_FILE=/run/secrets/pg_usr

secrets:
  pg_usr:
    file: ./pg_usr.txt
  pg_psswrd:
    file: ./pg_psswrd.txt
```
