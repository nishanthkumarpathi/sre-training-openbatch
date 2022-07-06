# Entrypoint Command

In this lesson, we will begin working with the ENTRYPOINT instruction. Though ENTRYPOINT functions very similarly to CMD it's behaviors are very different.

ENTRYPOINT allows us to configure a container that will run as an executable.
We can override all elements specified using CMD.
Using the docker run --entrypoint flag will override the ENTRYPOINT instruction.

Step 1: Setup your environment:

```bash
mkdir entrypoint
```

```bash
cd entrypoint
```

Step 2: Clone the image:

```bash
git clone https://github.com/nishanthkumarpathi/content-weather-app.git src
```

Step 3: Create the Dockerfile:

```bash
vi Dockerfile
```

Step 3: Create an image for the weather-app

Dockerfile contents:

```bash
FROM node
LABEL org.label-schema.version=v1.1
ENV NODE_ENV="production"
ENV PORT 3001

RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE $PORT
ENTRYPOINT ./bin/www
```

Step 4: Build the image:

```bash
docker image build -t nishanthkp/weather-app:v4 .
```

Step 5: Deploy the weather-app:

```bash
docker container run -d --name weather-app4 nishanthkp/weather-app:v4
```


Step 6: Inspect weather-app4:

```bash
docker container inspect weather-app4 | grep Cmd
```

```bash
docker container inspect weather-app-nonroot
```

```bash
docker container inspect weather-app4
```

Step 7: Create the weather-app container:

```bash
docker container run -d --name weather-app5 -p 8083:3001 nishanthkp/weather-app:v4 echo "Hello World"
```

Step 8: Inspect weather-app5:

```bash
docker container inspect weather-app5
```


Step 9: Create the volumes for Prometheus:

```bash
docker volume create prometheus
```

```bash
docker volume create prometheus_data
```

```bash
sudo chown -R nfsnobody:nfsnobody /var/lib/docker/volumes/prometheus/
```

```bash
sudo chown -R nfsnobody:nfsnobody /var/lib/docker/volumes/prometheus_data/
```


Step 10: Create the Prometheus container:

```bash
docker run --name prometheus -d -p 8084:9090 \
  -v prometheus:/etc/prometheus \
  -v prometheus_data:/prometheus/data \
  prom/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/prometheus/data
```

Step 11: Inspect Prometheus:

```bash
docker container inspect prometheus
```

Prometheus Dockerfile

https://github.com/prometheus/prometheus/blob/master/Dockerfile