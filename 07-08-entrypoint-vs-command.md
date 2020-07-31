# Entrypoint vs command

In this lesson, we will begin working with the `ENTRYPOINT` instruction. Though `ENTRYPOINT` functions very similarly to `CMD` it's behaviors are vary different.

`ENTRYPOINT` allows us to configure a container that will run as an executable.
We can override all elements specified using `CMD`.
Using the `docker run --entrypoint` flag will override the `ENTRYPOINT` instruction.
Setup your environment:
```
cd docker_images
mkdir entrypoint
cd entrypoint
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
ENV PORT 3001

RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE $PORT
ENTRYPOINT ./bin/www
```

Clone the image:
```
git clone https://github.com/linuxacademy/content-weather-app.git src
```

Build the image:
```
docker image build -t linuxacademy/weather-app:v4 .
```

Deploy the weather-app:
```
docker container run -d --name weather-app4 linuxacademy/weather-app:v4
```

Inspect weather-app4:
```
docker container inspect weather-app4 | grep Cmd
docker container inspect weather-app-nonroot
docker container inspect weather-app4
```

Create the weather-app container:
```
docker container run -d --name weather-app5 -p 8083:3001 linuxacademy/weather-app:v4 echo "Hello World"
```

Inspect weather-app5:
```
docker container inspect weather-app5
```

Create the volumes for Prometheus:
```
docker volume create prometheus
docker volume create prometheus_data

sudo chown -R nfsnobody:nfsnobody /var/lib/docker/volumes/prometheus/
sudo chown -R nfsnobody:nfsnobody /var/lib/docker/volumes/prometheus_data/
```

Create the Prometheus container:
```
docker run --name prometheus -d -p 8084:9090 \
  -v prometheus:/etc/prometheus \
  -v prometheus_data:/prometheus/data \
  prom/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/prometheus/data
```

Inspect Prometheus:
```
docker container inspect prometheus
```
