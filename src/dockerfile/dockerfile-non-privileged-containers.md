# Non-privileged Containers

In this lesson, you will learn how to use the USER instruction to create a non-privileged user. Rather than using root, we can use a non-privileged user to configure and run an application.

# Simple Non Privileged Container

Step 1: Setup your environment:


```bash
mkdir non-privileged-user
```

```bsh
cd non-privileged-user
```

Step 2: Create the Dockerfile:

```bash
vi Dockerfile
```

Step 3: Creates a CentOS image that uses cloud_user as a non-privileged user

Dockerfile contents:

```bash
FROM centos:latest
RUN useradd -ms /bin/bash cloud_user
USER cloud_user
```

Step 4: Build the new image:

```bash
docker image build -t centos7/nonroot:v1 .
```

Step 5: Create a container using the new image:

```bash
docker container run -it --name test-build centos7/nonroot:v1 /bin/bash
```

Step 6: Connecting as a privileged user:

```bash
docker container start test-build
```

```bash
docker container exec -u 0 -it test-build /bin/bash
```

# Node.JS Based Application Non Privileged Container

Step 1: Set up the environment:

```bash
mkdir node-non-privileged-user
```

```bash
cd node-non-privileged-user
```

Step 2: Clone the Github Repository

```bash
git clone https://github.com/nishanthkumarpathi/content-weather-app.git src
```


Step 3: Create the Dockerfile:

```bash
vi Dockerfile
```


Step 4: Create an image for the weather-app

Dockerfile contents:

```bash
FROM node
LABEL org.label-schema.version=v1.1
RUN useradd -ms /bin/bash node_user
USER node_user
ADD src/ /home/node_user
WORKDIR /home/node_user
RUN npm install
EXPOSE 3000
CMD ./bin/www
```

Step 5: Build the weather-app image using the non-privileged user node_user:

```bash
docker image build -t nishanthkp/weather-app-nonroot:v1 .
```

Step 6: Create a container using the nishanthkp/weather-app-nonroot:v1 image:

```bash
docker container run -d --name weather-app-nonroot -p 8086:3000 nishanthkp/weather-app-nonroot:v1
```