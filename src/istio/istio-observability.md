# Istio Observability

## Istio Observability Setup

Istio integrates with [several](https://istio.io/latest/docs/ops/integrations) different telemetry applications. These can help you gain an understanding of the structure of your service mesh, display the topology of the mesh, and analyze the health of your mesh.

Use the following instructions to deploy the [Kiali](https://istio.io/latest/docs/ops/integrations/kiali/) dashboard, along with [Prometheus](https://istio.io/latest/docs/ops/integrations/prometheus/), [Grafana](https://istio.io/latest/docs/ops/integrations/grafana), and [Jaeger](https://istio.io/latest/docs/ops/integrations/jaeger/).

Install [Kiali and the other addons](https://github.com/istio/istio/tree/release-1.13/samples/addons) and wait for them to be deployed.

```
kubectl apply -f samples/addons
```

```
kubectl rollout status deployment/kiali -n istio-system
```

Ensure everything is running fine , Go to LENS software and check it.

## Kiali Dashboard Access

```
istioctl dashboard kiali
```

View your Kiali Dashboard in your Browser.

In the left navigation menu, select _Graph_ and in the _Namespace_ drop down, select _default_.

> Use `ctrl+c` to break out.

## Prometheus Dashboard Access

Verify that the `prometheus` service is running in your cluster.

```
kubectl -n istio-system get svc prometheus
```

Open the Prometheus UI, execute the following command:

```
istioctl dashboard prometheus
```

Click **Graph** to the right of Prometheus in the header.

### Execute a Prometheus query.

In the “Expression” input box at the top of the web page, enter the text:

```
istio_requests_total
```

Then, click the **Execute** button.

![Sample: Prometheus Query Result](<../.gitbook/assets/image (1) (1).png>)

You can also see the query results graphically by selecting the Graph tab underneath the **Execute** button.

![Sample Prometheus Query Result - Graphical](<../.gitbook/assets/image (1).png>)

### Other queries to try:

*   Total count of all requests to the `productpage` service:

    ```
    istio_requests_total{destination_service="productpage.default.svc.cluster.local"}
    ```
*   Total count of all requests to `v3` of the `reviews` service:

    ```
    istio_requests_total{destination_service="reviews.default.svc.cluster.local", destination_version="v3"}
    ```

    This query returns the current total count of all requests to the v3 of the `reviews` service.
*   Rate of requests over the past 5 minutes to all instances of the `productpage` service:

    ```
    rate(istio_requests_total{destination_service=~"productpage.*", response_code="200"}[5m])
    ```

> Use `ctrl+c` to break out.

## Grafana Dashboard Access

Verify that the Grafana service is running in your cluster.

In Kubernetes environments, execute the following command:

```
kubectl -n istio-system get svc grafana
```

In Kubernetes environments, execute the following command:

```
istioctl dashboard grafana
```

Visit [http://localhost:3000](http://localhost:3000/d/G8wLrJIZk/istio-mesh-dashboard) your web browser.

> Use `ctrl+c` to break out.

## Jaeger Dashboard Access

Verify that the Jaeger service is running in your cluster.

In Kubernetes environments, execute the following command:

```
kubectl -n istio-system get svc jaeger-collector
```

In Kubernetes environments, execute the following command:

```
istioctl dashboard jaeger
```

Visit [ ](http://localhost:16686/jaeger/search)[http://localhost:16686/jaeger/search](http://localhost:16686/jaeger/search) your web browser.

> Use `ctrl+c` to break out.

## Troubleshooting

Ensure you have the following path setup from Previous Section

Step3: Add the `istioctl` client to your path (Linux or macOS):

```
export PATH=$PWD/bin:$PATH
```

## Istio Cleanup / Uninstall

The Istio uninstall deletes the RBAC permissions and all resources hierarchically under the `istio-system` namespace. It is safe to ignore errors for non-existent resources because they may have been deleted hierarchically.

```
kubectl delete -f samples/addons
```

```
istioctl manifest generate --set profile=demo | kubectl delete --ignore-not-found=true -f -
```

```
istioctl tag remove default
```

The `istio-system` namespace is not removed by default. If no longer needed, use the following command to remove it:

```
kubectl delete namespace istio-system
```

The label to instruct Istio to automatically inject Envoy sidecar proxies is not removed by default. If no longer needed, use the following command to remove it:

```
kubectl label namespace default istio-injection-
```

