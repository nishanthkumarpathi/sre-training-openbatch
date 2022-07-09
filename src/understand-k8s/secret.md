# Secrets

The kubernetes.io/basic-auth type is provided for storing credentials needed for basic authentication. 

When using this Secret type, the data field of the Secret must contain the following two keys:

- username: the user name for authentication;
- password: the password or token for authentication.

Both values for the above two keys are base64 encoded strings. 

You can, of course, provide the clear text content using the stringData for Secret creation.

1. Create a Basic Auth Secret

```bash
kubectl apply -f basic-auth-secret.yaml
```

2. Get the Secrets List

```bash
kubectl get secrets
```

3. You can view a description of the Secret

```bash
kubectl describe secrets/secret-basic-auth
```
