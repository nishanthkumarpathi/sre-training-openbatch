# Docker Compose Commands

In this lesson, we will start using compose by creating a compose file. Then we will create and manage the services by using the most commonly used commands:

build: Build or rebuild services
bundle: Generate a Docker bundle from the Compose file
config: Validate and view the Compose file
create: Create services
down: Stop and remove containers, networks, images, and volumes
events: Receive real time events from containers
exec: Execute a command in a running container
help: Get help on a command
images: List images
kill: Kill containers
logs: View output from containers
pause: Pause services
port: Print the public port for a port binding
ps: List containers
pull: Pull service images
push: Push service images
restart: Restart services
rm: Remove stopped containers
run: Run a one-off command
scale: Set number of containers for a service
start: Start services
stop: Stop services
top: Display the running processes
unpause: Unpause services
up: Create and start containers
version: Show the Docker-Compose version information

# Instructions

Step 1: Setup your environment:

```bash
mkdir -p compose/commands
```

```bash
cd compose/commands
```

Step 2: Create a docker-compose file:

```bash
vi docker-compose.yml
```

docker-compose.yml contents:

```yml
version: '3'
services:
  web:
    image: nginx
    ports:
    - "8080:80"
    volumes:
    - nginx_html:/usr/share/nginx/html/
    links:
    - redis
  redis:
    image: redis
volumes:
  nginx_html: {}
```

Step 4: Create a compose service:

```bash
docker-compose up -d
```

Step 5: List containers created by compose:

```bash
docker-compose ps
```

Step 6: Stopping a compose service:

```bash
docker-compose stop
```

Step 7: Starting a compose service:


```bash
docker-compose start
```

Step 8: Restarting a compose service:

```bash
docker-compose restart
```

Step 9: Delete a compose service:

```bash
docker-compose down
```
