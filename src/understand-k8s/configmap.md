# Configmap

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.

Caution: ConfigMap does not provide secrecy or encryption. If the data you want to store are confidential, use a Secret rather than a ConfigMap, or use additional (third party) tools to keep your data private.

1. ConfigMap that has some keys with single values, and other keys where the value looks like a fragment of a configuration format.

```bash
kubectl apply -f app-configmap.yaml
```

2. Pod that uses values from "game-demo" Configmap to configure a Pod:

```bash
kubectl apply -f read-configmap-using-pod.yaml
```

3. Login to the Pod to view the Mounted Configmaps

```bash
kubectl exec -it configmap-demo-pod sh
```
