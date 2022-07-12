# Persistent Volume Claim

In this section, we will take a look at Persistent Volume Claim

Now we will create a Persistent Volume Claim to make the storage available to the node.

Volumes and Persistent Volume Claim are two separate objects in the Kubernetes namespace.

Once the Persistent Volume Claim created, Kubernetes binds the Persistent Volumes to claim based on the request and properties set on the volume.

### Persistent Volume

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

```bash
kubectl get pv
```
If properties not matches or Persistent Volume is not available for the Persistent Volume Claim then it will display the pending state.

### Persistent Volume Claim

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

```bash
kubectl get pvc
```

### Delete Persistent Volume Claim

```bash
kubectl delete pvc myclaim
```

### Delete Persistent Volume

```bash
kubectl delete pv pv-vol1
```