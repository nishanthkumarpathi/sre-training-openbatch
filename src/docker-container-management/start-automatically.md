# Containers Start Automatically

In this lesson, we will look at how to set restart policies for containers, and how that will effect their behavior when the docker service is restarted.

To configure the restart policy for a container, use the --restart flag:

no: Do not automatically restart the container. (the default) on-failure: Restart the container if it exits due to an error, which manifests as a non-zero exit code. always: Always restart the container if it stops. unless-stopped: Similar to always, except that when the container is stopped, it is not restarted even after the Docker daemon restarts.

Automatically Restarting a container:

docker container run -d --name --restart&#x20;

Step 1: Make sure a container always restarts:

```bash
docker container run -d --name always-restart --restart always rivethead42/weather-app:latest
```

Step 2: Make sure a container restarts unless it's stopped:

```bash
docker container run -d --name unless-stopped --restart unless-stopped rivethead42/weather-app:latest
```

Step 3: Stop and restart your Docker service:

```bash
sudo systemctl restart docker
```

Step 4: List your containers:

```bash
docker container ls
```

Step 5: Stop the unless-stopped container:

```bash
docker container stop unless-stopped
```

Step 6: Stop and restart your Docker service:

```bash
sudo systemctl restart docker
```

Step 7: List your containers:

```bash
docker container ls
```

Step 8: Stop the unless-stopped container:

```bash
docker container stop always-restart
```

Step 9: Stop and restart your Docker service:

```bash
sudo systemctl restart docker
```

Step 10: List your containers:

```bash
docker container ls
```
