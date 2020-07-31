# Distributing image on dockerhub

In this lesson, we'll walk through how to tag and push an image to Docker Hub. You will need a Docker Hub account.

Create a Docker Hub account:
```
https://hub.docker.com/
```

Docker Push:
```
docker image push <USERNAME>/<IMAGE_NAME>:<TAG>
```

Creating an image for Docker Hub:
```
docker image tag <IMAGE_NAME>:<TAG> <linuxacademy>/<IMAGE_NAME>:<TAG>
```

Set up your environment:
```
cd docker_images
mkdir dockerhub
cd dockerhub
```

Create the Dockerfile:
```
vi Dockerfile
```

Dockerfile contents:
```
# Create an image for the weather-app using multi-stage build
FROM node AS build
RUN mkdir -p /var/node/
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install

FROM node:alpine
ARG VERSION=V1.1
LABEL org.label-schema.version=$VERSION
ENV NODE_ENV="production"
COPY --from=build /var/node /var/node
WORKDIR /var/node
EXPOSE 3000
ENTRYPOINT ["./bin/www"]
```

Git the weather-app code:
```
git clone https://github.com/linuxacademy/content-weather-app.git src
```

Use the Git commit hash as the image tag:
```
cd src
git log -1 --pretty=%H
cd ../
```

Build the image:
```
docker image build -t <USERNAME>/weather-app:<HASH> --build-arg VERSION=1.5 .
```

Tag the image before pushing it to Docker Hub:
```
docker image tag linuxacademy/weather-app:<HASH> <USERNAME>/weather-app:<HASH>
```

Push the image to Docker Hub:
```
docker login 
docker image push <USERNAME>/weather-app:<HASH>
```

Tag the latest image:
```
docker image tag <USERNAME>/weather-app:<HASH> <USERNAME>/weather-app:latest
```

Push the latest image to Docker Hub:
```
docker login <USERNAME>
docker image push <USERNAME>/weather-app:latest
```