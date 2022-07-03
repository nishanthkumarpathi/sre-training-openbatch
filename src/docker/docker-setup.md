# Docker Setup


## Set up the repository

Update the apt package index and install packages to allow apt to use a repository over HTTPS:

```bash
sudo apt-get update
```

```bash
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

```

## Add Docker’s official GPG key:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. Learn about nightly and test channels.

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```


## Install Docker Engine

Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:

```bash
sudo apt-get update
```

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Manage Docker as a non-root user
Add your user to the docker group.

```bash
sudo usermod -aG docker $USER
```

Log out and log back in so that your group membership is re-evaluated.

If testing on a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.

On a desktop Linux environment such as X Windows, log out of your session completely and then log back in.

```bash
newgrp docker
```

# Create a Dockerhub Account

Next Create a Dockerhub Account.