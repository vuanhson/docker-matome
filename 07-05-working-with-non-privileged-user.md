# Working with non privileged user

In this lesson, you will learn how to use the `USER` instruction to create a non-privileged user. Rather than using root, we can use a non-privileged user to configure and run an application.

Setup your environment:
```
cd docker_images
mkdir non-privileged-user
cd non-privileged-user
```

Create the Dockerfile:
```
vi Dockerfile
```

Dockerfile contents:
```
# Creates a CentOS image that uses cloud_user as a non-privileged user
FROM centos:latest
RUN useradd -ms /bin/bash cloud_user
USER cloud_user
```
The next RUN, ENTRYPOINT, CMD... will be run as this user

Build the new image:
```
docker image build -t centos7/nonroot:v1 .
```

Create a container using the new image:
```
docker container run -it --name test-build centos7/nonroot:v1 /bin/bash
```

Connecting as a privileged user:
```
docker container start test-build
docker container exec -u 0 -it test-build /bin/bash
```

Set up the environment:
```
cd ~/docker_images
mkdir node-non-privileged-user
cd node-non-privileged-user
```

Create the Dockerfile:
```
vi Dockerfile
```

Dockerfile contents:
```
# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
RUN useradd -ms /bin/bash node_user
USER node_user
ADD src/ /home/node_user
WORKDIR /home/node_user
RUN npm install
EXPOSE 3000
CMD ./bin/www
```
```
git clone https://github.com/linuxacademy/content-weather-app.git src
```

Build the `weather-app` image using the non-privileged user node_user:
```
docker image build -t linuxacademy/weather-app-nonroot:v1 .
```

Create a container using the linuxacademy/weather-app-nonroot:v1 image:
```
docker container run -d --name weather-app-nonroot -p 8086:3000 linuxacademy/weather-app-nonroot:v1
```