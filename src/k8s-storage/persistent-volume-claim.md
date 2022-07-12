# Persistent Volume Claim

If properties not matches or Persistent Volume is not available for the Persistent Volume Claim then it will display the pending state.

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