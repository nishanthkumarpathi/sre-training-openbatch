# Deployments

* A Deployment named `nginx-deployment` is created, indicated by the `.metadata.name` field.
* The Deployment creates three replicated Pods, indicated by the `.spec.replicas` field.
*   The `.spec.selector` field defines how the Deployment finds which Pods to manage. In this case, you select a label that is defined in the Pod template (`app: nginx`). However, more sophisticated selection rules are possible, as long as the Pod template itself satisfies the rule.

Before you begin, make sure your Kubernetes cluster is up and running. Follow the steps given below to create the above Deployment:


1.  Create the Deployment by running the following command:

```bash
kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml
```

2. Run `kubectl get deployments` to check if the Deployment was created.

```bash
kubectl get deployments
```

* When you inspect the Deployments in your cluster, the following fields are displayed:

    * `NAME` lists the names of the Deployments in the namespace.
    * `READY` displays how many replicas of the application are available to your users. It follows the pattern ready/desired.
    * `UP-TO-DATE` displays the number of replicas that have been updated to achieve the desired state.
    * `AVAILABLE` displays how many replicas of the application are available to your users.
    * `AGE` displays the amount of time that the application has been running.



    Notice how the number of desired replicas is 3 according to `.spec.replicas` field.
*

    1. To see the Deployment rollout status, run `kubectl rollout status deployment/nginx-deployment`.

    ```bash
    kubectl rollout status deployment/nginx-deployment
    ```



    The output is similar to:

    ```
    Waiting for rollout to finish: 2 out of 3 new replicas have been updated...
    deployment "nginx-deployment" successfully rolled out
    ```



    1. Run the `kubectl get deployments` again a few seconds later. 
```bash
kubectl get deployments
```



Notice that the Deployment has created all three replicas, and all replicas are up-to-date (they contain the latest Pod template) and available.



1.  To see the ReplicaSet (`rs`) created by the Deployment, run `kubectl get rs`. 

```bash
kubectl get rs
```

The output is similar to this:

    ```
    NAME                          DESIRED   CURRENT   READY   AGE
    nginx-deployment-75675f5897   3         3         3       18s
    ```

To see the labels automatically generated for each Pod.

```
kubectl get pods --show-labels
```
