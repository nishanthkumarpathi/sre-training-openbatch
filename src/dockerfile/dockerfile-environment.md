# Dockerfile Environment Variables

To make new software easier to run, you can use ENV to update the PATH environment variable for the software that your container installs.

## Setup your environment:

Step 1: Make the env Directory

```bash
mkdir env
```

```bash
cd env
```

Use the --env flag to pass an environment variable when building an image:

--env [KEY]=[VALUE]

Use the ENV instruction in the Dockerfile:

ENV [KEY]=[VALUE]  
ENV [KEY] [VALUE]

Step 1: Clone the weather-app:

```bash
git clone https://github.com/nishanthkumarpathi/content-weather-app.git src
```

Step 2: Create the Dockerfile

```bash
vi Dockerfile
```

# Create an image for the weather-app

Step 3: Dockerfile contents:

```bash
FROM node
LABEL org.label-schema.version=v1.1
ENV NODE_ENV="development"
ENV PORT 3000

RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE $PORT
CMD ./bin/www
```


Step 4: Create the weather-app container:

```bash
docker image build -t nishanthkp/weather-app:v2 .
```

Step 5: Inspect the container to see the environment variables:

```bash
docker image inspect nishanthkp/weather-app:v2
```

Step 6: Deploy the weather-dev application:

```bash
docker container run -d --name weather-dev -p 8082:3001 --env PORT=3001 nishanthkp/weather-app:v2
```

Step 7: Inspect the development container to see the environment variables:

```bash
docker container inspect weather-dev
```

Step 8: Deploy the weather-app to production:

```bash
docker container run -d --name weather-app2 -p 8083:3001 --env PORT=3001 --env NODE_ENV=production nishanthkp/weather-app:v2
```

Step 9: Inspect the production container to see the environment variables:

```bash
docker container inspect weather-app2
```

Step 10: Get the logs for weather-app2:

```bash
docker container logs weather-app2
```

```bash
docker container run -d --name weather-prod -p 8084:3000 --env NODE_ENV=production nishanthkp/weather-app:v2
```
