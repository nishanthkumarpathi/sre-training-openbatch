# Service NodePort

# Service NodePort

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
 type: NodePort
 ports:
 - targetPort: 80
   port: 80
   nodePort: 30008
 selector:
   run: myapp
```

### Curl or Wget

```bash
wget http://<nodeport-ip:port>
```

```bash
curl http://<nodeport-ip:port>
```