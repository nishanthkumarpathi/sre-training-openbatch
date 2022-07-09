# Service Cluster IP

Applications running in a Kubernetes cluster find and communicate with each other, and the outside world, through the Service abstraction

We are using a Nginx webserver that echoes back the source IP of requests it receives through an HTTP header.

1. Create a Nginx WebServer with echoserver Image

```bash
kubectl create deployment web-app --image=k8s.gcr.io/echoserver:1.4
```

1. Expose the echoserver Image pod with the help of a service.

```bash
kubectl expose deployment web-app --name=web-app-svc --port=80 --target-port=8080
```

1. Get the Service IP Address

```bash
kubectl get svc web-app-svc
```

1. Run a Client Server to test Cluster IP

```bash
kubectl run busybox -it --image=busybox --restart=Never --rm
```

Inside the Busy Box Image, we are going to run the below commands.

1. Check the IP Address of the Client.

```bash
ip addr
```

1. Use Wget to call the Web-app-svc from the Busybox Pod

Replace "10.0.170.92" with the IPv4 address of the Service named "web-app-svc"

```bash
wget -qO - 10.0.170.92
```

If you observe the output has "client\_address"

The client\_address is always the client pod's IP address, whether the client pod and server pod are in the same node or in different nodes

Run nslookup to the above web-app-svc to know the fully qualified domain name

### Cleanup

1. Delete Service and Deployment

```bash
kubectl delete svc web-app-svc
```

```bash
kubectl delete deployment web-app
```
