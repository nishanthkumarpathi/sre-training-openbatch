# Secrets

The kubernetes.io/basic-auth type is provided for storing credentials needed for basic authentication. 

When using this Secret type, the data field of the Secret must contain the following two keys:

- username: the user name for authentication;
- password: the password or token for authentication.

Both values for the above two keys are base64 encoded strings. 

You can, of course, provide the clear text content using the stringData for Secret creation.

### Create a Secret

```yml
apiVersion: v1
kind: Secret
metadata:  
  name: newsecret
type: Opaque
data:
  username: dXNlcg==
  password: NTRmNDFkMTJlOGZh
```


### Use Secret in the Pod

```yml
apiVersion: v1
kind: Pod
metadata:
  name: test-pod
spec:
  containers:
    - name: test-pod
      image: redis
      volumeMounts:
      - name: newsecret
        mountPath: "/etc/newsecret"
        readOnly: true
  volumes:
  - name: newsecret
    secret:
      secretName: newsecret
```