# Environment Variables

To make new software easier to run, you can use ENV to update the PATH environment variable for the software that your container installs.

Setup your environment:
```
cd docker_images
mkdir env
cd env
```

Use the --env flag to pass an environment variable when building an image:
```
--env [KEY]=[VALUE]
```

Use the ENV instruction in the Dockerfile:
```
ENV [KEY]=[VALUE]  
ENV [KEY] [VALUE]
```

Clone the weather-app:
```
git clone https://github.com/linuxacademy/content-weather-app.git src
```

Create the Dockerfile
```
vi Dockerfile
```

Dockerfile contents:
```
# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
ENV NODE_ENV="development"
ENV PORT 3000

RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE $PORT
CMD ./bin/www
```

Create the `weather-app` container:
```
docker image build -t linuxacademy/weather-app:v2 .
```

Inspect the container to see the environment variables:
```
docker image inspect linuxacademy/weather-app:v2
```

Deploy the `weather-dev` application:
```
docker container run -d --name weather-dev -p 8082:3001 --env PORT=3001 linuxacademy/weather-app:v2
```

Inspect the development container to see the environment variables:
```
docker container inspect weather-dev
```

Deploy the `weather-app` to production:
```
docker container run -d --name weather-app2 -p 8083:3001 --env PORT=3001 --env NODE_ENV=production linuxacademy/weather-app:v2
```

Inspect the production container to see the environment variables:
```
docker container inspect weather-app2
```

Get the logs for weather-app2:
```
docker container logs weather-app2
```

```
docker container run -d --name weather-prod -p 8084:3000 --env NODE_ENV=production linuxacademy/weather-app:v2
```
