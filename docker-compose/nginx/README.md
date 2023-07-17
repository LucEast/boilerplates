# Example for NGINX

## Create a Docker Network

```bash
docker network create --driver bridge --subnet=192.168.2.0/24 --gateway=192.168.2.1 nginx-test-net
```

## Create Docker Volume

```bash
docker volume create --name nginx-test-volume --opt type=none --opt device=/etc/docker/container/nginx-test/volume --opt o=bind
```

## Create .env File

```
#docker-compose
COMPOSE_PATH_SEPARATOR=:
COMPOSE_FILE=docker-compose.yml:docker-network.yml
```

## create docker-network.yml

```yml
version: '3.8'

networks:
    {NETWORK}:
        external: true
```

## Create docker-compose.yml

```yml
version: '3.8'

services:
    {SERVICE}:
        image: {IMAGE}
        container_name: {CONRAINER_NAME}
        ports: 
            - 8080:80
        volumes:
            - {VOLUME}
        networks:
            - {NETWORK}
        
volumes:
    {VOLUME}:
```