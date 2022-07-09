# Service NodePort


Applications running in a Kubernetes cluster find and communicate with each other, and the outside world, through the Service abstraction

We are using a Nginx webserver that echoes back the source IP of requests it receives through an HTTP header.

1. Create a Nginx WebServer with echoserver Image

```bash
kubectl create deployment web-app --image=k8s.gcr.io/echoserver:1.4
```

2. Expose the echoserver Image pod with the help of a service.

```bash
kubectl expose deployment web-app --name=web-app-svc --port=80 --target-port=8080 --type=NodePort
```

3. Get the Service IP Address

```bash
kubectl get svc web-app-svc
```

4. Run a Client Server to test NodePort Connectivity

```bash
kubectl run busybox -it --image=busybox --restart=Never --rm
```
Inside the Busy Box Image, we are going to run the below commands.

5. Check the IP Address of the Client.

```bash
ip addr
```
6. Use Wget to call the Web-app-svc from the Busybox Pod

Replace "10.0.170.92" with the IPv4 address of the Kubernetes Worker Node and Port which is in 30000 range.

```bash
wget -qO - 10.0.170.92:30171
```

If you observe the output has "client_address"

The client_address is not always the client pod's IP address. there a natting done, when it is sent to Destination. 

### Cleanup

7. Delete Service and Deployment

```bash
kubectl delete svc web-app-svc
```

```bash
kubectl delete deployment web-app
```

