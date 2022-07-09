# Pod Connectivity

### How to deploy pods?

Lets now take a look to create a nginx pod using **`kubectl`**.

Step 1: To deploy a docker container by creating a POD.

```
kubectl run webapp --image nginx
```

Step 2: To get the list of pods

```
kubectl get pods
```

Step 3: Run the command **`kubectl describe pod <<podname>>`**look under the containers section.

```
kubectl describe pod webapp
```

```
kubectl delete pod webapp
```

Step 4: Create a pod definition YAML file and use it to create a POD or use the command **`kubectl run webapp-pod --image=nginx`**.

```
kubectl run webapp-pod --image=nginx --dry-run=client -o yaml > webapp-pod.yaml
```

```
kubectl create -f webapp-pod.yaml
```

Step 5: View the Manifest and the file would like something like this or you can modify the file as below. Some not important structure is removed from the original file.

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: webapp
  name: webapp-pod
spec:
  containers:
  - image: nginx
    name: webapp-container
  restartPolicy: Always
```
