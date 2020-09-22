# Common docker container
## Portainer-for manage image and container basic level
1. On command line

```bash
# https://www.portainer.io/installation/

docker volume create portainer_data

docker run -d --name=portainer --restart=always -p 8000:8000 -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

## Adminer - for manage database
1. On command line
```bash
docker run -d --name=adminer --restart=always -p 9001:8080 adminer
```

2. On docker-compose

```yaml
version: '3'
services:
  adminer:
    image: adminer
    restart: always
    ports:
      - 9000:8080
```

default ip database base on docker: 172.17.0.1
check by
## PostgreSQL
1. On 1 command

```bash
# 1. create volumes
docker volume create postgres_data
# then
docker run -d --name postgresdb --restart=always -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres  -v postgres_data:/var/lib/postgresql/data -p 5432:5432 postgres:11.4-alpine
# or
docker run -d --name postgresdb --restart=always -e POSTGRES_USER=postgres -v postgres_data:/var/lib/postgresql/data -p 5432:5432 postgres:11.4-alpine
```

2. docker-composer file

```yml
version: "3"
services:
  db:
    image: "postgres:11.4-alpine"
    container_name: "postgresdb"
    restart: always
    environment:
      - POSTGRES_USER: postgres
      # - POSTGRES_PASSWORD:
    ports:
      - "54320:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
volumes:
  postgres_data:
```

## hoppscotch - API interactive/ API document
https://github.com/hoppscotch/hoppscotch
docker run -d --name postwoman --restart=always  -p 9001:3000 postwoman:latest


# install docker by one command
# 1. create volumes

docker volume create mysql8_data
# then
docker run -d --name mysql8 --restart=always -e MYSQL_USER=bn_wordpress -e  MYSQL_PASSWORD=44b0294923  -e MYSQL_ROOT_PASSWORD=password -v mysql8_data:/var/lib/mysql -p 3307:3306 mysql:8.0.21 --default_authentication_plugin=mysql_native_password
