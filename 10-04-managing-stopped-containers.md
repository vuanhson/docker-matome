# Managing stopped containers

In this lesson, we will manage stopped containers by starting, deleting, or pruning them.

Remove one or more containers:
```
docker container rm <NAME>
```

List the rm flags:
```
docker container rm -h
```

Start one or more stopped containers:
```
docker container start <NAME>
```

Remove all stopped containers:
```
docker container prune
```

List the IDs of all containers:
```
docker container ls -a -q
```

List all stopped containers:
```
docker container ls -a -f status=exited
```

List the IDs of stopped containers:
```
docker container ls -a -q -f status=exited
```

Get a count of all stopped containers:
```
docker container ls -a -q -f status=exited | wc -l
```

Get a listing of our containers:
```
docker container ls -a -f status=exited | grep prometheus
```

Start Prometheus:
```
docker container start prometheus
```

Find stopped weather-app containers with grep:
```
docker container ls -a -f status=exited | grep weather-app
```

Remove stopped weather-app containers:
```
docker container rm [CONTAINER_IDS]
```

Prune all stopped containers:
```
docker container prune
```