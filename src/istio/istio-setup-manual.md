# Istio Setup Manual

## Pull the Containers in all the nodes

{% hint style="info" %}
If you have rate limiting issues, then ensure all necessary images are already downloaded on to the master and worker nodes.
{% endhint %}

This guide lets you quickly evaluate Istio. If you are already familiar with Istio or interested in installing other configuration profiles or advanced [deployment models](https://istio.io/latest/docs/ops/deployment/deployment-models/), refer to our [which Istio installation method should I use?](https://istio.io/latest/about/faq/#install-method-selection) FAQ page.

These steps require you to have a cluster running a [supported version](https://istio.io/latest/docs/releases/supported-releases#support-status-of-istio-releases) of Kubernetes (1.20, 1.21, 1.22, 1.23). You can use any supported platform, for example [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) or others specified by the [platform-specific setup instructions](https://istio.io/latest/docs/setup/platform-setup/).

### Download Istio <a href="#download" id="download"></a>

Step1: Go to the [Istio release](https://github.com/istio/istio/releases/tag/1.13.3) page to download the installation file for your OS, or download and extract the latest release automatically (Linux or macOS):

```
curl -L https://istio.io/downloadIstio | sh -
```

The command above downloads the latest release (numerically) of Istio

Step2: Add the `istioctl` client to your path (Linux or macOS):

```
sudo cp istio-1.13.3/bin/istioctl /usr/bin/
```

```
istioctl version
```

if you do the above steps correctly, it will print the output.

Step 3: Move to the Istio package directory. For example, if the package is `istio-1.13.3`:

Try to run this command using Git Bash

```bash
cd istio-1.13.3
```

The installation directory contains:

* Sample applications in `samples/`
* The [`istioctl`](https://istio.io/latest/docs/reference/commands/istioctl) client binary in the `bin/` directory.

### Install Istio <a href="#install" id="install"></a>

Step 1: For this installation, we use the `minimal`[configuration profile](https://istio.io/latest/docs/setup/additional-setup/config-profiles/). It’s selected to have a good set of defaults for testing, but there are other profiles for production or performance testing.

```bash
istioctl install --set profile=demo -y
```

Step 2: Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later:

```bash
kubectl label namespace default istio-injection=enabled
```
