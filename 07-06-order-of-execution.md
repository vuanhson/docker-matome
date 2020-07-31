# Order of Execution

This lesson focuses on the order that instructions are executed in when building an image. Some instructions may have unintended consequences that can cause your build to fail.

Setup your environment:
```
cd docker_images
mkdir centos-conf
cd centos-conf
```

Create the Dockerfile:
```
vi Dockerfile
```

Dockerfile contents:
```
# Creates a CentOS image that uses cloud_user as a non-privileged user
FROM centos:latest
RUN mkdir -p ~/new-dir1
RUN useradd -ms /bin/bash cloud_user
USER cloud_user
RUN mkdir -p ~/new-dir2
RUN mkdir -p /etc/myconf        <- Error because cloud_user don't have permission
RUN echo "Some config data" >> /etc/myconf/my.conf
```

Build the new image:
```
docker image build -t centos7/myconf:v1 .
```