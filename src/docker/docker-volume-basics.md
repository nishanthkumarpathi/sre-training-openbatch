# Docker Volume Basics

Volumes are the preferred method of maintaining persistent data in Docker. In this lesson, we will begin learning how to use the volume subcommand to list, create, and remove volumes.

Step 1: List all Docker volume commands:

```bash
docker volume -h
```

create: Create a volume.
inspect: Display detailed information on one or more volumes.
ls: List volumes.
prune: Remove all unused local volumes.
rm: Remove one or more volumes.

Step 2: List all volumes on a host:

```bash
docker volume ls
```

Step 3: Create two new volumes:

```bash
docker volume create test-volume1
```

```bash
docker volume create test-volume2
```

Step 4: Get the flags available when creating a volume:

```bash
docker volume create -h
```

Step 5: Inspecting a volume:

```bash
docker volume inspect test-volume1
```

Step 6: Deleting a volume:

```bash
docker volume rm test-volume
```

Removing all unused volumes:

```bash
docker volume prune
```