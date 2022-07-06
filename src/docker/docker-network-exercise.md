# Docker Network Exercise

In this lesson, we will dig deeper into container networking by supplying our own subnet and gateway when creating a new network. We will then move on to networking two different containers using an internal network. This will allow one container to be publicly accessible while the other one is not.

## Creating a network and defining a Subnet and Gateway

Step 1: Create a bridge network with a subnet and gateway:

```bash
docker network create --subnet 10.1.0.0/24 --gateway 10.1.0.1 br02
```

Step 2: Run ifconfig to view the bridge interface for br02:

```bash
ifconfig
```

Step 3: Inspect the br02 network:

```bash
docker network inspect br02
```

Step 4: Prune all unused networks:

```bash
docker network prune
```

## Create a network with an IP range:

```bash
docker network create --subnet 10.1.0.0/16 --gateway 10.1.0.1 \
--ip-range=10.1.4.0/24 --driver=bridge --label=host4network br04
```

Step 1: Inspect the br04 network:

```bash
docker network inspect br04
```

Step 2: Create a container using the br04 network:

```bash
docker container run --name network-test01 -it --network br04 centos /bin/bash
```


## Install Net Tools:

```bash
yum update -y
```

```bash
yum install -y net-tools
```


Get the IP info for the container:

```bash
ifconfig
```

Get the gateway info the container:

```bash
netstat -rn
```

Get the DNS info for the container:

```bash
cat /etc/resolv.conf
```


Assigning IPs to a container:


Create a new container and assign an IP to it:


```bash
docker container run -d --name network-test02 --ip 10.1.4.102 --network br04 nginx
```


Get the IP info for the container:

```bash
docker container inspect network-test02 | grep IPAddr
```


## Networking two containers

Step 1: Create an internal network:

```bash
docker network create -d bridge --internal localhost
```

Step 2: Create a MySQL container that is connected to localhost:

```bash
docker container run -d --name test_mysql \
-e MYSQL_ROOT_PASSWORD=P4sSw0rd0 \
--network localhost mysql:5.7
```

Step 3: Create a container that can ping the MySQL container:

```bash
docker container run -it --name ping-mysql \
--network bridge \
centos
```

Step 4: Connect ping-mysql to the localhost network:

```bash
docker network connect localhost ping-mysql
```

Step 5: Restart and attach to container:

```bash
docker container start -ia ping-mysql
```

Step 6: Create a container that can't ping the MySQL container:

```bash
docker container run -it --name cant-ping-mysql \
centos
```

Step 7: Create a Nginx container that is not publicly accessible:

```bash
docker container run -d --name private-nginx -p 8081:80 --network localhost nginx
```

Step 8: Inspect private-nginx:

```bash
docker container inspect private-nginx
```