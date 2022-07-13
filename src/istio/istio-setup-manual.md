# Istio Setup Manual

### Step 1: Download Istio <a href="#download" id="download"></a>

Step1: Go to the [Istio release](https://github.com/istio/istio/releases/tag/1.13.3) page to download the installation file for your OS, or download and extract the latest release automatically (Linux or macOS):

![](<../.gitbook/assets/image (5).png>)

Step 2: Unzip the IstioCtl and then Place the isitoctl.exe file in your "c" drive Kubetools folder.

![](<../.gitbook/assets/image (4).png>)

Step 3: On the Desktop, Create a folder to work on the lab files.

![](<../.gitbook/assets/image (2).png>)

### Install Istio <a href="#install" id="install"></a>

Step 1: For this installation, we use the `minimal`[configuration profile](https://istio.io/latest/docs/setup/additional-setup/config-profiles/). It’s selected to have a good set of defaults for testing, but there are other profiles for production or performance testing.

```bash
istioctl install --set profile=demo -y
```

Step 2: Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later:

```bash
kubectl label namespace default istio-injection=enabled
```

```
istioctl analyze
```
