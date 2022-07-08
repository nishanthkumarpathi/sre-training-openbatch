# Docker Compose Install

Step 1: To download and install Compose standalone, run:

```bash
curl -SL https://github.com/docker/compose/releases/download/v2.6.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
```

Step 2: Apply executable permissions to the standalone binary in the target path for the installation.

```bash
chmod +x /usr/local/bin/docker-compose
```

Step 3: Test and execute compose commands using docker-compose.

```bash
docker-compose --version
```

[]: # Language: markdown
[]: # Path: src\docker-compose\docker-compose-usage.md