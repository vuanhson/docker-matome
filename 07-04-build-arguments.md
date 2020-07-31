# Build Arguments

In this lesson, we will explore using build arguments to paramerterize an image build.

Use the --build-arg flag when building an image:
```
--build-arg [NAME]=[VALUE]
```

Use the ARG instruction in the Dockerfile:
```
ARG [NAME]=[DEFAULT_VALUE]
```

Navigate to the args directory:
```
cd docker_images
mkdir args
cd args
```

Clone the weather-app:
```
git clone https://github.com/linuxacademy/content-weather-app.git src
```

Create the Dockerfile:
```
vi Dockerfile
```

Dockerfile:
```
# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
ARG SRC_DIR=/var/node       (Note: Default value is /var/node if not supply when build)

RUN mkdir -p $SRC_DIR
ADD src/ $SRC_DIR
WORKDIR $SRC_DIR
RUN npm install
EXPOSE 3000
CMD ./bin/www
```

Create the weather-app container:
```
docker image build -t linuxacademy/weather-app:v3 --build-arg SRC_DIR=/var/code .
```

Inspect the image:
```
docker image inspect linuxacademy/weather-app:v3 | grep WorkingDir
```

Create the weather-app container:
```
docker container run -d --name weather-app3 -p 8085:3000 linuxacademy/weather-app:v3
```

Verify that the container is working by executing curl:
```
curl localhost:8085
```
