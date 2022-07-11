# Rolling Updates and Rollback

Deployment  for Rolling Update Strategies

```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: myapp-deployment
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-container
           image: nginx
     replicas: 3
     selector:
       matchLabels:
        type: front-end
```

You can see the status of the rollout by the below command

```bash
kubectl rollout status deployment/myapp-deployment
```

To see the history and revisions

```bash
kubectl rollout history deployment/myapp-deployment
```

### myapp-deployment

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
 name: myapp-deployment
 labels:
  app: nginx
spec:
 template:
   metadata:
     name: myap-pod
     labels:
       app: myapp
       type: front-end
   spec:
    containers:
    - name: nginx-container
      image: nginx:1.7.1
 replicas: 3
 selector:
  matchLabels:
    type: front-end
```

### To undo a change

```bash
kubectl rollout undo deployment/myapp-deployment
```
