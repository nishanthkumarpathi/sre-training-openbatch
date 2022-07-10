# Service Cluster IP

### Deployment File

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
  labels:
    run: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      run: myapp
  template:
    metadata:
      labels:
        run: myapp
    spec:
      containers:
      - name: myapp-container
        image: nginx
        ports:
        - containerPort: 80
```

### Service File

```yml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: ClusterIP
  ports:
    - targetPort: 80
      port: 80
  selector:
    run: myapp
```

### Busybox Container

```bash
kubectl run busybox -it --image=busybox --restart=Never --rm
```