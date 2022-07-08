# Docker Compose File

In this lesson we will look at the basics of creating a compose file.

Step 1: Setup your environment:

cd compose
git clone https://github.com/linuxacademy/content-weather-app.git weather-app
cd weather-app
git checkout compose

Step 2: Create a docker-compose.yml file:

```bash
vi docker-compose.yml
```

docker-compose.yml contents:

```yml
version: '3'
services:
  weather-app:
    build:
      context: .
      args:
        - VERSION=v2.0
    ports:
      - "8081:3000"
    environment:
      - NODE_ENV=production
```

Step 3: Create the compose container:

```bash
docker-compose up -d
```

List compose services:

```bash
docker-compose ps
```


Step 4: Verify the weather-app is working:

```bash
curl http://localhost:8081
```


Step 5: Rebuild the image:

```bash
docker-compose build
```

Step 6: Rebuild the image with no cache:

```bash
docker-compose build --no-cache
```


