# Persistent Volume

A Persistent Volume is a cluster-wide pool of storage volumes configured by an administrator to be used by users deploying application on the cluster. The users can now select storage from this pool using Persistent Volume Claims.

File name : pv-definition.yaml

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

```bash
kubectl delete pv pv-vol1
```


