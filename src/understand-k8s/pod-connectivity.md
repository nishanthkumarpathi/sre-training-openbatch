# Pod Connectivity

### How to deploy pods?

Lets now take a look to create a nginx pod using **`kubectl`**.

*   To deploy a docker container by creating a POD.

    ```
    kubectl run nginx --image nginx
    ```



*   To get the list of pods

    ```
    kubectl get pods
    ```


* Run the command **`kubectl describe pod <<podname>>`**look under the containers section.

Create a pod definition YAML file and use it to create a POD or use the command **`kubectl run myapp-pod --image=nginx`**.

```
kubectl run myapp-pod --image=nginx --dry-run=client -o yaml > myapp-pod.yaml
```
