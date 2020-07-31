# Using dockerignore

In this lesson, we'll create a `.dockerignore` file, so that we can exclude files we don't want copied over when building an image.

Setup your environment:
```
cd docker_images
mkdir dockerignore
cd dockerignore
git clone https://github.com/linuxacademy/content-weather-app.git src
cd src
git checkout dockerignore
cd ../
```

Create the `.dockerignore` file:
```
vi .dockerignore
```

Add the following to `.dockerignore`:
```
# Ignore these files
*/*.md
*/.git
src/docs/
*/tests/
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
ENV NODE_ENV="production"
ENV PORT 3000

RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE $PORT
ENTRYPOINT ["./bin/www"]
```

Build the image:
```
docker image build -t linuxacademy/weather-app:v5 .
```

Create the weather-app container:
```
docker container run -d --name weather-app-ignore linuxacademy/weather-app:v5
```

List the contents of /var/node:
```
docker container exec weather-app-ignore ls -la /var/node
```