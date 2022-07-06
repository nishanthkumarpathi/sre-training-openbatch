# Dockerfile Order of Execution


This lesson focuses on the order that instructions are executed in when building an image. Some instructions may have unintended consequences that can cause your build to fail.

Step 1: Setup your environment:

```bash
mkdir centos-conf
```

```bash
cd centos-conf
```


Step 2: Create the Dockerfile:

```bash
vi Dockerfile
```

Step 3: Creates a CentOS image that uses cloud_user as a non-privileged user

Dockerfile contents:

```bash
FROM centos:latest
RUN mkdir -p ~/new-dir1
RUN useradd -ms /bin/bash cloud_user
USER cloud_user
RUN mkdir -p ~/new-dir2
RUN mkdir -p /etc/myconf
RUN echo "Some config data" >> /etc/myconf/my.conf
```


Step 4: Build the new image:

```bash
docker image build -t centos7/myconf:v1 .
```


