# Volume commands

Volumes are the preferred method of maintaining persistent data in Docker. In this lesson, we will begin learning how to use the volume subcommand to list, create, and remove volumes.

## Volume Basics
List all Docker volume commands:
```
docker volume -h
```

- `create`: Create a volume.
- `inspect`: Display detailed information on one or more volumes.
- `ls`: List volumes.
- `prune`: Remove all unused local volumes.
- `rm`: Remove one or more volumes.

List all volumes on a host:
```
docker volume ls
```

Create two new volumes:
```
docker volume create test-volume1
docker volume create test-volume2
```

Get the flags available when creating a volume:
```
docker volume create -h
```

Inspecting a volume:
```
docker volume inspect test-volume1
```

Deleting a volume:
```
docker volume rm test-volume
```

Removing all unused volumes:
```
docker volume prune
```