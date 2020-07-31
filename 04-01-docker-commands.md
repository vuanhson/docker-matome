# Docker commands

In this lesson we will start working with Docker commands. We'll see the management commands, along with the ones for managing images and containers.

Get a list of all of the Docker commands:
```
docker -h
```

Management command were introduced in Docker engine v1.13

There are changes from old command like `docker ps` to new management command, describle below:

Management Commands:
- `builder` Manage builds
- `config` Manage Docker configs
- `container` Manage containers
- `engine` Manage the docker engine
- `image` Manage images
- `network` Manage networks
- `node` Manage Swarm nodes
- `plugin` Manage plugins
- `secret` Manage Docker secrets
- `service` Manage services
- `stack` Manage Docker stacks
- `swarm` Manage Swarm
- `system` Manage Docker
- `trust` Manage trust on Docker images
- `volume` Manage volumes

`docker image`:
- `build` Build an image from a dockerfile
- `history` Show the history of an image
- `import` Import the contents from a tarball to create a filesystem image
- `inspect` Display detailed information on one or more images
- `load` Load an image from a tar file or STDIN
- `ls` List images
- `prune` Remove unused images
- `pull` Pull an image or a repository from a registry
- `push` Push an image or a repository to a registry
- `rm` Remove one or more images
- `save` Save one or more images to a tar file (streamed to STDOUT by default)
- `tag` Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

`docker container`:
- `attach` Attach local standard input, output, and error streams to a running container
- `commit` Create a new image from a container's changes
- `cp` Copy files/folders between a container and the local filesystem
- `create` Create a new container
- `diff` Inspect changes to files or directories on a container's filesystem
- `exec` Run a command in a running container
- `export` Export a container's filesystem as a tar archive
- `inspect` Display detailed information on one or more containers
- `kill` Kill one or more running containers
- `logs` Fetch the logs of a container
- `ls` List containers
- `pause` Pause all processes within one or more containers
- `port` List port mappings or a specific mapping for the container
- `prune` Remove all stopped containers
- `rename` Rename a container
- `restart` Restart one or more containers
- `rm` Remove one or more containers
- `run` Run a command in a new container
- `start` Start one or more stopped containers
- `stats` Display a live stream of container(s) resource usage statistics
- `stop` Stop one or more running containers
- `top` Display the running processes of a container
- `unpause` Unpause all processes within one or more containers
- `update` Update configuration of one or more containers
- `wait` Block until one or more containers stop, then print their exit codes

Eg:

Run docker in detach mode, open random port
```
docker container run -P -d nginx:latest
```

View container process:
```
docker container top <container_id>
```

Start stopped container:
```
docker container start <container_id>
```

View logs
```
docker container logs <container_id>
```

Attach into container
```
docker container exec -it <container_id> /bin/bash
```
If you just want to exec a command, you can replace `/bin/bash` with the command you want


View consuming resource of a container:
```
docker container stats <container_id>
```
