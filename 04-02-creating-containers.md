# Creating containers

In this lesson, we will take a deeper look into creating containers, by exploring a few of the flags that will alter it's behavior when created.

`docker container run`:
- `--help` Print usage
- `--rm` Automatically remove the container when it exits
- `-d`, `--detach` Run container in background and print container ID
- `-i`, `--interactive` Keep STDIN open even if not attached
- `--name string` Assign a name to the container
- `-p`, `--publish list` Publish a container's port(s) to the host
- `-t`, `--tty` Allocate a pseudo-TTY
- `-v`, `--volume list` Mount a volume (the bind type of mount)
- `--mount mount` Attach a filesystem mount to the container
- `--network string` Connect a container to a network (default "default")

Create a container and attach to it:
```
docker container run –it busybox
```

Create a container and run it in the background:
```
docker container run –d nginx
```

Create a container that you name and run it in the background:
```
docker container run –d –name myContainer busybox
```