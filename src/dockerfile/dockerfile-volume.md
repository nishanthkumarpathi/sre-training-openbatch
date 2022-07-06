# Dockerfile Volume

In this lesson, we will use the VOLUME instruction to automatically create a mount point in a Docker image. When a container is created using this image, a volume will be created and mounted to the specified directory.

Step 1: Set up your environment:

```bash
mkdir volumes
```

```bash
cd volumes

```

Step 2: Create the Dockerfile:

```bash
vi Dockerfile
```

Step 3: Build an Nginx image that uses a volume:


```bash
FROM nginx:latest
VOLUME ["/usr/share/nginx/html/"]
```

Step 4: Build the new image:

```bash
docker image build -t nishanthkp/nginx:v1 .
```


Step 5: Create a new container using the nishanthkp/nginx:v1 image:
```bash
docker container run -d --name nginx-volume nishanthkp/nginx:v1
```


Step 6: Inspect nginx-volume:
```bash
docker container inspect nginx-volume
```


Step 7: List the volumes:

```bash
docker volume ls | grep [VOLUME_NAME]
```


Step 8: Inspect the volumes:
```bash
docker volume inspect [VOLUME_NAME]
```