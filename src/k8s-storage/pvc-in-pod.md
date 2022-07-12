# PVC in POD

In this section, we will take a look at Using PVC in PODs

In this case, Pods access storage by using the claim as a volume. Persistent Volume Claim must exist in the same namespace as the Pod using the claim.

The cluster finds the claim in the Pod's namespace and uses it to get the Persistent Volume backing the claim. The volume is then mounted to the host and into the Pod.

Persistent Volume is a cluster-scoped and Persistent Volume Claim is a namespace-scoped.

### Create a Persistent Volume Claim

File Name : pv-definition.yaml

```yaml
kind: PersistentVolume
apiVersion: v1
metadata:
    name: pv-vol1
spec:
    accessModes: [ "ReadWriteOnce" ]
    capacity:
     storage: 1Gi
    hostPath:
     path: /tmp/data
```

```bash
kubectl create -f pv-definition.yaml
```

### Create a Persistent Volume Claim

File Name : pvc-definition.yaml

```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: myclaim
spec:
  accessModes: [ "ReadWriteOnce" ]
  resources:
   requests:
     storage: 1Gi
```

```bash
kubectl create -f pvc-definition.yaml
```

### Create a Pod using PVC

File Name : pod-definition.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: web
  volumes:
    - name: web
      persistentVolumeClaim:
        claimName: myclaim
```

    
```bash
kubectl create -f pod-definition.yaml
```

### List PV, PVC, and POD

```bash
kubectl get pod,pvc,pv
```



