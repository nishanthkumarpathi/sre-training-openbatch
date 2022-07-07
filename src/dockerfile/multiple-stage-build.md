# Multiple Stage Build


In this lesson, we will learn how to build smaller images using multi-stage builds.

By default, the stages are not named
Stages are numbered with integers
Starting with 0 for the first FROM instruction
Name the stage by adding as to the FROM instruction
Reference the stage name in the COPY instruction


Step 1: Set up your environment:

```bash
cd docker_images
```

```bash
mkdir multi-stage-builds
```

```bash
cd multi-stage-builds
```

```bash
git clone https://github.com/nishanthkumarpathi/content-weather-app.git src
```

Step 2: Create the Dockerfile:

```bash
vi Dockerfile
```

Step 3: Create an image for the weather-app using multi-stage build

Dockerfile contents:

```Dockerfile
FROM node AS build
RUN mkdir -p /var/node/
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install

FROM node:alpine
ARG VERSION=V1.1
LABEL org.label-schema.version=$VERSION
ENV NODE_ENV="production"
COPY --from=build /var/node /var/node
WORKDIR /var/node
EXPOSE 3000
ENTRYPOINT ["./bin/www"]
```

Step 4: Create an image for the weather-app using multi-stage build


```bash
docker image build -t nishanthkp/weather-app:multi-stage-build --rm --build-arg VERSION=1.5 .
```

Step 5: List images to see the size difference:

```bash
docker image ls
```

Step 6: Create the weather-app container:

```bash
docker container run -d --name multi-stage-build -p 8087:3000 nishanthkp/weather-app:multi-stage-build
```
