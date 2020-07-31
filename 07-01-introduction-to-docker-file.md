# Introduction to docker file

In this lesson we will start learning about building images using a Dockerfile.

## What is the Dockerfile?
Dockerfiles are instructions. They contains all of the commands used to build an image.
- Docker images consist of read-only layers.
- Each represents a Dockerfile instruction.
- Layers are stacked.
- Each layer is a result of the changes from the previous layer.
- Images are built using the docker image build command.

## Dockerfile Layers
```
Dockerfile:  
FROM ubuntu:15.04  
COPY . /app  
RUN make /app  
CMD python /app/app.py
```

`FROM` creates a layer from the ubuntu:15.04 Docker image.
`COPY` adds files from your Docker client’s current directory.
`RUN` builds your application with make.
`CMD` specifies what command to run within the container.

## Best Practices
General guidelines:
- Keep containers as ephemeral as possible.
- Follow Principle 6 of the 12 Factor App.
- Avoid including unnecessary files.
- Use `.dockerignore`
- Use multi-stage builds.
- Don’t install unnecessary packages.
- Decouple applications. (Do not include multiple applications in one container, eg. wordpress vs MySQL)
- Minimize the number of layers.
- Sort multi-line arguments.
- Leverage build cache.