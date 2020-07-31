# Working with instructions

`FROM`: Initializes a new build stage and sets the Base Image

`RUN`: Will execute any commands in a new layer

`CMD`: Provides a default for an executing container. There can only be one CMD instruction in a Dockerfile

`LABEL`: Adds metadata to an image

`EXPOSE`: Informs Docker that the container listens on the specified network ports at runtime

`ENV`: Sets the environment variable <key> to the value <value>

`ADD`: Copies new files, directories or remote file URLs from <src> and adds them to the filesystem of the image at the path <dest>.

`COPY`: Copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>.

`ENTRYPOINT`: Allows for configuring a container that will run as an executable

`VOLUME`: Creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers

`USER`: Sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any RUN, CMD, and ENTRYPOINT instructions that follow it in the Dockerfile

`WORKDIR`: Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY, and ADD instructions that follow it in the Dockerfile

`ARG`: Defines a variable that users can pass at build-time to the builder with the docker build command, using the --build-arg <varname>=<value> flag

`ONBUILD`: Adds a trigger instruction to the image that will be executed at a later time, when the image is used as the base for another build

`HEALTHCHECK`: Tells Docker how to test a container to check that it is still working

`SHELL`: Allows the default shell used for the shell form of commands to be overridden

To set up the environment:
```
sudo yum install git -y
mkdir docker_images
cd docker_images
mkdir weather-app
cd weather-app
git clone https://github.com/linuxacademy/content-weather-app.git src
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
RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE 3000
CMD ./bin/www
```

Build the weather-app image:
```
docker image build -t linuxacademy/weather-app:v1 .
```

List the images:
```
docker image ls
```

Create the weather-app container:
```
docker container run -d --name weather-app1 -p 8081:3000 linuxacademy/weather-app:v1
```

List all running containers:
```
docker container ls
```

Difference between ADD and COPY: https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy