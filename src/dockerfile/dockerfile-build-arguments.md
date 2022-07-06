# Dockerfile Build Arguments

In this lesson, we will explore using build arguments to paramerterize an image build.

Use the --build-arg flag when building an image:

--build-arg [NAME]=[VALUE]

Use the ARG instruction in the Dockerfile:

ARG [NAME]=[DEFAULT_VALUE]

Step 1: Navigate to the args directory:

```bash
mkdir args
```

```bash
cd args
```

Step 2: Clone the weather-app:

```bash
git clone https://github.com/nishanthkumarpathi/content-weather-app.git src
```

Step 3: Create the Dockerfile:

```bash
vi Dockerfile
```



Step 4: Create an image for the weather-app

Dockerfile:


```bash
FROM node
LABEL org.label-schema.version=v1.1
ARG SRC_DIR=/var/node

RUN mkdir -p $SRC_DIR
ADD src/ $SRC_DIR
WORKDIR $SRC_DIR
RUN npm install
EXPOSE 3000
CMD ./bin/www
```


Step 5: Build the weather-app image:

```bash
docker image build -t nishanthkp/weather-app:v3 --build-arg SRC_DIR=/var/code .
```


Step 6: Inspect the image:

```bash
docker image inspect nishanthkp/weather-app:v3 | grep WorkingDir
```

Step 7: Create the weather-app container:


```bash
docker container run -d --name weather-app3 -p 8085:3000 nishanthkp/weather-app:v3
```

Step 8: Verify that the container is working by executing curl:

```bash
curl localhost:8085
```

In case if you dont find curl in your system, then do the following.

```bash
sudo apt install curl
```