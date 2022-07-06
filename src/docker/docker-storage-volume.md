# Docker Storage

Using Volumes for Persistent Storage

In this lesson, we will take a deeper look into using volumes with our Docker containers. Volumes are the preferred method for maintaining persistent data.

Volumes are easier to back up or migrate than bind mounts. You can manage volumes using Docker CLI commands or the Docker API. They work on both Linux and Windows containers. Volumes can be more safely shared among multiple containers. Volume drivers allow for:

- Storing volumes on remote hosts or cloud providers
- Encrypting the contents of volumes
- Add other functionality
- New volumes can have their content pre-populated by a container.

Step 1: Create a new volume for an Nginx container:

```bash
docker volume create html-volume
```

Step 2: Creating a volume using that volume mount:

```bash
docker container run -d \
 --name nginx-volume1 \
 --mount type=volume,source=html-volume,target=/usr/share/nginx/html/ \
 nginx
```


Step 3: Inspect the volume:

```bash
docker volume inspect html-volume
```

Step 4: List the contents of html-volume:

```bash
sudo ls /var/lib/docker/volumes/html-volume/_data
```

Step 5: Creating a volume using that volume flag:

```bash
docker container run -d \
 --name nginx-volume2 \
 -v html-volume:/usr/share/nginx/html/ \
 nginx
```

Step 6: Edit index.html:

```bash
sudo vi /var/lib/docker/volumes/html-volume/_data/index.html
```

Step 7: Inspect nginx-volume2 to get the private IP:

```bash
docker container inspect nginx-volume2
```

Step 8: Login into nginx-volume1 and go to the html directory:

```bash
docker container exec -it nginx-volume1 /bin/bash
```

```bash
cd /usr/share/nginx/html
```

```bash
cat index.hml
```
Install Vim:

```bash
apt-get update -y
```

```bash
apt-get install vim -y
```

Step 9: Using a readonly volume:

```bash
docker run -d \
  --name=nginx-volume3 \
  --mount source=html-volume,target=/usr/share/nginx/html,readonly \
  nginx
```

Step 10: Login into nginx-volume3 and go to the html directory:

```bash
docker container exec -it nginx-volume3 /bin/bash
```

```bash
cd /usr/share/nginx/html
```

```bash
cat index.hml
```
Install Vim:

```bash
apt-get update -y
```
```bash
apt-get install vim -y
```