# Service LoadBalancer

1. Run a Hello World application in your cluster:

```bash
kubectl apply -f https://raw.githubusercontent.com/nishanthkumarpathi/k8s-calico-istio-training/main/understand-k8s/services/load-balancer-example.yaml
```

The preceding command creates a Deployment and an associated ReplicaSet. The ReplicaSet has five Pods each of which runs the Hello World application.

1. Display information about the Deployment:

```bash
kubectl get deployments hello-world
```

```bash
kubectl describe deployments hello-world
```

1. Display information about your ReplicaSet objects:

```bash
kubectl get replicasets
```

```bash
kubectl describe replicasets
```

1. Create a Service object that exposes the deployment:

```bash
kubectl expose deployment hello-world --type=LoadBalancer --name=my-service
```

1. Display information about the Service:

```bash
kubectl get services my-service
```

1. Display detailed information about the Service:

```bash
kubectl describe services my-service
```

In the preceding output, you can see that the service has several endpoints: 10.0.0.6:8080,10.0.1.6:8080,10.0.1.7:8080 + 2 more. These are internal addresses of the pods that are running the Hello World application.

1. To verify these are pod addresses, enter this command:

```bash
kubectl get pods --output=wide
```

1. Use the external IP address (LoadBalancer Ingress) to access the Hello World application:

curl http://:

or

go to browser and type the Load Balancer IP Ingress IP Address.

## Cleaning up

To delete the Service, enter this command:

```bash
kubectl delete services my-service
```

To delete the Deployment, the ReplicaSet, and the Pods that are running the Hello World application, enter this command:

```bash
kubectl delete deployment hello-world
```
