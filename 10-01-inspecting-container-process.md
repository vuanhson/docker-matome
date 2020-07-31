# Inspecting container process

In this lesson, we'll take a look at a few ways we can examine the running processes in a container.

Docker Top:
```
docker container top <NAME>
```

Docker Stats:
```
docker container stats <NAME>
```

Create a new CentOS container:
```
docker container run -itd --name container_process centos /bin/bash
```

Execute `docker container top`:
```
docker container top container_process
```

Attach to `container_process`:
```
docker container exec -it container_process /bin/bash
```

Attach to the container using `attach`:
```
docker container attach container_process
```

Restart the container:
```
docker container start container_process
```

Attach to the `container_process` container:
```
docker container exec -it container_process /bin/bash
```

Run top on the container:
```
top
exit
```

Get stats on a container:
```
docker container stats container_process
```