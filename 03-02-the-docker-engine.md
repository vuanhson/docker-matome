# The docker engine

## Under The Hood
Docker engine - heart of what run and manage containers
- Modular in design:
  - Batteries included but replaceable
- Based on open-standards outline by the Open Container Initiative
- The major components:
  - Docker client
  - Docker daemon
  - containerd
  - runc
- The components work together to create and run containers
![docker-engine](media/04-01.png)

## A Brief History of the Docker Engine
The first release of Docker:
- The Docker daemon:
  - Monolithic binary
  - Docker client
  - Docker API
  - Container runtime
  - Image builds
  - Much more...
- LXC: (Linux specific, cannot run on windows or mac)
  - Namespaces
  - Control groups (cgroups)
  - Linux-specific

Note: you can see other architecture describle images in slide inside documents folder

## Refactoring of the Docker Engine
LXC was later replaced with libcontainer (because LXC is an extra tool but it was very core to docker)
- Docker 0.9
- Platform agnostic

Issues with the monolithic Docker daemon:
- Harder to innovate
- Slow
- Not what the ecosystem wanted

Docker became more modular:
- Smaller more specialized tools
- Pluggable architecture

Open Container Initiative declared:
- Image spec
- Container runtime spec
- Version 1.0 release in 2017
- Docker Inc. heavily contributed
- Docker 1.11 (2016) used the specification as much as possible

`runc`
- Implemenation of the OCI container-runtime-spec
- Lightweght CLI wrapper for libcontainer
- Create containers

`containerd`
- Manages container lifecycle
  - Start
  - Stop
  - Pause
  - Delete
- Image management (push, pull)
- Part of the 1.11 release

`shim`
- Implemenation of daemonless Containers
- `containerd` forks an instance of runc for each new container
- `runc` process exits after the container is created
- `shim` process becomes the container parent
- Responsible for:
  - STDIN and STDOUT
  - Reporting exit status to the Docker daemon

## Running Containers
```
docker container run -it --name <NAME> <IMAGE>:<TAG>
```

Creating a container:
- CLI use for executing a command
- Docker client uses the appropriate API payload
- POSTs to the correct API endpoint
- Docker deamon receives instructions
- Docker deamon calls `containerd` to start a new container
- Docker daemon uses gRPC (a CRUD style API)
- `containerd` creates an OCI bundle from the Docker image
- Tells `runc` to create a container using the OCI bundle
- `runc` interfaces with the OS kernel to get the constructs needed to create a container
  - This includes namespaces, cgroups, etc.
- Container process starts as a child process
- `runc` exits once the container starts
- Process is complete, and container is running