# Managing Docker with Portainer

In this lesson, we'll install Portainer and use it manage our Docker host.

Create a volume for Portainers data:
```
docker volume create portainer_data
```

Create the Portainers container:
```
docker container run -d --name portainer -p 8080:9000 \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_data:/data portainer/portainer

docker container ls
```

The `ls` should output:
```
rivethead42/weather-app:latest
NODE_ENV production
```