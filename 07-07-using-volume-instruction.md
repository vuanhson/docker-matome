# Using volume instruction

In this lesson, we will use the VOLUME instruction to automatically create a mount point in a Docker image. When a container is created using this image, a volume will be created and mounted to the specified directory.

Set up your environment:
```
cd docker_images
mkdir volumes
cd volumes
```

Create the Dockerfile:
```
vi Dockerfile
```

Build an Nginx image that uses a volume:
```
FROM nginx:latest
VOLUME ["/usr/share/nginx/html/"]
```

Build the new image:
```
docker image build -t linuxacademy/nginx:v1 .
```

Create a new container using the linuxacademy/nginx:v1 image:
```
docker container run -d --name nginx-volume linuxacademy/nginx:v1
```

Inspect nginx-volume:
```
docker container inspect nginx-volume
```

List the volumes:
```
docker volume ls | grep [VOLUME_NAME]
```

Inspect the volumes:
```
docker volume inspect [VOLUME_NAME]
```
