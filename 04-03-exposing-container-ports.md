# Exposing container ports

## Exposing and Publishing Container Ports

Building on what we've already learned, this lesson will focus on exposing ports on a container, as well as how to publish them.

Exposing:
- Expose a port or a range of ports
- This does not publish the port
- Use `--expose [PORT]`
```
docker container run --expose 1234 [IMAGE]
```

Publishing:

- Maps a container's port to a host`s port
- `-p` or `--publish` publishes a container's port(s) to the host
- `-P`, or `--publish-all` publishes all exposed ports to random ports

```
docker container run -p [HOST_PORT]:[CONTAINER_PORT] [IMAGE]
docker container run -p [HOST_PORT]:[CONTAINER_PORT]/tcp -p [HOST_PORT]:[CONTAINER_PORT]/udp [IMAGE]
docker container run -P
```

Lists all port mappings or a specific mapping for a container:
```
docker container port [Container_NAME]
```