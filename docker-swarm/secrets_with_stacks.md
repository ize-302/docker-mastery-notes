# Secrets with stacks

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

## from existing file. [Should only be done during development. No recommended for prod]
secrets:
  pg_usr:
    file: ./pg_usr.txt
  pg_psswrd:
    file: ./pg_psswrd.txt

#OR

## from secrets attached to the service via the cli
secrets:
  pg_usr:
    external: true
  pg_psswrd:
    external: true
```

### deploying the stack

```bash
docker stack deploy -c docker-compose.yml mydb
```

### removing the stack

This will also automatically remove the secrets

```bash
docker stack rm mydb
```

NOTE: keeping secrets in files is only recommended in local development for security reasons
