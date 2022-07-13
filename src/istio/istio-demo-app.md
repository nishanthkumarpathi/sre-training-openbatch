# Istio Demo App



If you are following the guide sequentially, all necessary requriments are met from the previous section of lab. However if you are starting from the Middle of lab guide. Please ensure the following are met.

* Istioctl is configured properly and path is already set.

## Profile Configuration

For this installation, we use the `demo` [configuration profile](https://istio.io/latest/docs/setup/additional-setup/config-profiles/). It’s selected to have a good set of defaults for testing, but there are other profiles for production or performance testing.

```
istioctl install --set profile=demo -y
```

## Deploy the sample application <a href="#bookinfo" id="bookinfo"></a>

Deploy the [`Bookinfo` sample application](https://istio.io/latest/docs/examples/bookinfo/)

```
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
```

The application will start. As each pod becomes ready, the Istio sidecar will be deployed along with it.

```
kubectl get services
```

and

```
kubectl get pods
```

Verify everything is working correctly up to this point



## Open the application to outside traffic <a href="#ip" id="ip"></a>

The Bookinfo application is deployed but not accessible from the outside. To make it accessible, you need to create an [Istio Ingress Gateway](https://istio.io/latest/docs/concepts/traffic-management/#gateways), which maps a path to a route at the edge of your mesh.

1.  Associate this application with the Istio gateway:

    ```
    kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml
    ```


2.  Ensure that there are no issues with the configuration:

    ```
    istioctl analyze
    ```



{% hint style="info" %}
Determining the ingress IP and ports, by visiting the Services Section.&#x20;

If required make a productpage services as NodePort
{% endhint %}

## Determining the ingress IP and ports <a href="#determining-the-ingress-ip-and-ports" id="determining-the-ingress-ip-and-ports"></a>

Follow these instructions to set the `INGRESS_HOST` and `INGRESS_PORT` variables for accessing the gateway. Use the tabs to choose the instructions for your chosen platform:



Set the ingress ports:

```
export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')
```

```
export SECURE_INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="https")].nodePort}')
```

Ensure a port was successfully assigned to each environment variable:

```
echo "$INGRESS_PORT"
```

```
echo "$SECURE_INGRESS_PORT"
```

Set the ingress IP ( Using sredemo cluster name to Identify cluster ip )

```
export INGRESS_HOST=$(minikube ip -p sredemo)
```

Ensure an IP address was successfully assigned to the environment variable:

```
echo "$INGRESS_HOST"
```

Set `GATEWAY_URL`:

```
export GATEWAY_URL=$INGRESS_HOST:$INGRESS_PORT
```

Ensure an IP address and port were successfully assigned to the environment variable:

```
echo "$GATEWAY_URL"
```
