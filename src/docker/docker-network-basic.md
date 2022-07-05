# Docker Network Basics


In this lab you'll look at the most basic networking components that come with a fresh installation of Docker.

You will complete the following steps as part of this lab.

- [Step 1 - The `docker network` command](#docker_network)
- [Step 2 - List networks](#list_networks)
- [Step 3 - Inspect a network](#inspect)
- [Step 4 - List network driver plugins](#list_drivers)

# Prerequisites

You will need all of the following to complete this lab:

- A Linux-based Docker Host running Docker 1.12 or higher

# <a name="docker_network"></a>Step 1: The `docker network` command

The `docker network` command is the main command for configuring and managing container networks.

Run a simple `docker network` command from any of your lab machines.

```
docker network

Usage:  docker network COMMAND

Manage Docker networks

Options:
      --help   Print usage

Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  rm          Remove one or more networks

Run 'docker network COMMAND --help' for more information on a command.
```

The command output shows how to use the command as well as all of the `docker network` sub-commands. As you can see from the output, the `docker network` command allows you to create new networks, list existing networks, inspect networks, and remove networks. It also allows you to connect and disconnect containers from networks.

# <a name="list_networks"></a>Step 2: List networks

Run a `docker network ls` command to view existing container networks on the current Docker host.

```
docker network ls

NETWORK ID          NAME                DRIVER              SCOPE
1befe23acd58        bridge              bridge              local
726ead8f4e6b        host                host                local
ef4896538cc7        none                null                local
```

The output above shows the container networks that are created as part of a standard installation of Docker.

New networks that you create will also show up in the output of the `docker network ls` command.

You can see that each network gets a unique `ID` and `NAME`. Each network is also associated with a single driver. Notice that the "bridge" network and the "host" network have the same name as their respective drivers.

# <a name="inspect"></a>Step 3: Inspect a network

The `docker network inspect` command is used to view network configuration details. These details include; name, ID, driver, IPAM driver, subnet info, connected containers, and more.

Use `docker network inspect` to view configuration details of the container networks on your Docker host. The command below shows the details of the network called `bridge`.

```
docker network inspect bridge

[
    {
        "Name": "bridge",
        "Id": "1befe23acd58cbda7290c45f6d1f5c37a3b43de645d48de6c1ffebd985c8af4b",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Containers": {},
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```

> **NOTE:** The syntax of the `docker network inspect` command is `docker network inspect <network>`, where `<network>` can be either network name or network ID. In the example above we are showing the configuration details for the network called "bridge". Do not confuse this with the "bridge" driver.

### View Ubuntu Network Details

```bash
ifconfig
```

### List all Docker network commands:

```bash
docker network -h
```

### Command Summary: 

* connect - Connect a container to a network 
* create - Create a network 
* disconnect - Disconnect a container from a network 
* inspect - Display detailed information on one or more networks 
* ls - List networks 
* prune - Remove all unused networks 
* rm - Remove one or more networks


### List all Docker networks on the host:

```bash
docker network ls
```

```bash
docker network ls --no-trunc
```

### Getting detailed info on a network:

docker network inspect [NAME]

Creating a network:

```bash
docker network create br00
```

### Deleting a network:

docker network rm [NAME]

Remove all unused networks:

```bash
docker network prune
```

### Adding and Removing containers to a network

Step 1: Create a container with no network:

```bash
docker container run -d --name network-test03 -p 8081:80 nginx
```

Step 2: Create a new network:

```bash
docker network create br01
```

Step 3: Add the container to the bridge network:

```bash
docker network connect br01 network-test03
```


Step 4: Inspect network-test03 to see the networks:

```bash
docker container inspect network-test03
```


Step 5: Remove network-test03 from br01:

```bash
docker network disconnect br01 network-test03
```