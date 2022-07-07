# Docker Compose Volumes and Network

In this lesson, we will learn how to use volumes and networks in a docker compose file.

Step 1: Setup your environment:

mkdir -p compose/ghost
cd compose/ghost

Step 2: Create a docker-compose.yml file:

vi docker-compose.yml

docker-compose.yml:

```yml
version: '3'
services:
  ghost:
    container_name: ghost
    image: ghost:latest
    ports:
      - "80:2368"
    environment:
      - database__client=mysql
      - database__connection__host=mysql
      - database__connection__user=root
      - database__connection__password=P4SSw0rd0!
      - database__connection__database=ghost
    volumes:
      - ghost-volume:/var/lib/ghost
    networks:
      - ghost_network
      - mysql_network
    depends_on:
      - mysql

  mysql:
    container_name: mysql
    image: mysql:5.7
    environment:
      - MYSQL_ROOT_PASSWORD=P4SSw0rd0!
    volumes:
      - mysql-volume:/var/lib/mysql
    networks:
      - mysql_network

volumes:
  ghost-volume:
  mysql-volume:

networks:
  ghost_network:
  mysql_network:
```


Step 2: Create the compose container:

```bash
docker-compose up -d
```


Step 4: List compose services:

```bash
docker-compose ps
```

Step 5: List the volumes:

```bash
docker volumes ls
```

Step 6: List the volumes:

```bash
docker network ls
```

Docker Compose Documentation(https://docs.docker.com/compose/compose-file/compose-file-v3/#docker-compose-file-v3)