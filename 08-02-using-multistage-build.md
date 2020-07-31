# Using multi-stage builds

In this lesson, we will learn how to build smaller images using multi-stage builds.
- By default, the stages are not named
- Stages are numbered with integers
- Starting with 0 for the first FROM instruction
- Name the stage by adding as to the FROM instruction
- Reference the stage name in the COPY instruction

Set up your environment:
```
cd docker_images
mkdir multi-stage-builds
cd multi-stage-builds
git clone https://github.com/linuxacademy/content-weather-app.git src
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

Build the image:
```
docker image build -t linuxacademy/weather-app:multi-stage-build --rm --build-arg VERSION=1.5 .
```

List images to see the size difference:
```
docker image ls
```

Create the weather-app container:
```
docker container run -d --name multi-stage-build -p 8087:3000 linuxacademy/weather-app:multi-stage-build
```