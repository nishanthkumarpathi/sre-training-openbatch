# Calico Networking

### Create a single-node minikube cluster

Minikube offers a built-in Calico implementation, this is a quick way to checkout Calico features.

```bash
minikube start --network-plugin=cni --cni=calico
```

### Verify Calico installation
You can verify Calico installation in your cluster by issuing the following command.

```bash
watch kubectl get pods -l k8s-app=calico-node -A
```
Use ctrl+c to break out of watch.

Congratulations you now have a minikube cluster equipped with Calico

### Add an additional worker node

```bash
minikube node add
```
Verify nodes using the following command

```bash
minikube node list
```
