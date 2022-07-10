# K8s Installation

### K8s Setup Requirements

* 8 CPUs or more
* 16GB of free memory
* 150 GB of free disk space
* Internet connection
* Container or virtual machine manager, such as: Docker, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, or VMware Fusion/Workstation

### Install kubectl

Download the latest Kubectl release with the command:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

```
chmod +x kubectl
```

```
sudo mv kubectl /usr/bin/
```

Test to ensure the version you installed is up-to-date:

```bash
kubectl version
```

### Kubectl autocomplete <a href="#kubectl-autocomplete" id="kubectl-autocomplete"></a>

#### BASH <a href="#bash" id="bash"></a>

```bash
source <(kubectl completion bash) # setup autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.
```

You can also use a shorthand alias for `kubectl` that also works with completion:

```bash
alias k=kubectl
complete -o default -F __start_kubectl k
```

#### ZSH <a href="#zsh" id="zsh"></a>

```bash
source <(kubectl completion zsh)  # setup autocomplete in zsh into the current shell
echo '[[ $commands[kubectl] ]] && source <(kubectl completion zsh)' >> ~/.zshrc # add autocomplete permanently to your zsh shell
```

### Install Kubernetes using Minikube

To install the latest minikube stable release on x86-64 Linux using Debian package:

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
```

```bash
sudo dpkg -i minikube_latest_amd64.deb
```

### Start the Cluster

Start your minikube cluster with one master node using the following command.

We are using Flannel Plugin for Networking, NetworkPolicy Management, Traffic Management

```bash
minikube start --network-plugin=cni --cni=flannel
```

***

Use `ctrl+c` to break out of watch.

Congratulations you now have a minikube cluster equipped with Flannel

### Enable Metrics Server

```bash
minikube addons enable metrics-server
```

{% hint style="danger" %}
**Ensure your Master Node is in Healthy State and all the necessary services and pods are working fine.**
{% endhint %}

### **Worker Nodes Creation**

**Note**: This as an optional step, you can safely skip this step if you do not require an additional worker node.

```
minikube node add --worker=true
```

{% hint style="info" %}
Now login to the Worker node and then pull all the latest images that are required.

You can use the same script that is used in the Master Server from the above section.
{% endhint %}

Verify nodes using the following command

```
kubectl get nodes
```

Repeat the above steps, if you want to add more worker Nodes.

##
