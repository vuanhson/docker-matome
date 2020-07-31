# Working with services

In this lesson, we'll see how to create and manage a service running in Docker Swarm.

Docker service commands:

- `create`: Creates a new service
- `inspect`: Displays detailed information on one or more services
- `logs`: Fetches the logs of a service or task
- `ls`: Lists services
- `ps`: Lists the tasks of one or more services
- `rm`: Removes one or more services
- `rollback`: Reverts changes to a service's configuration
- `scale`: Scales one or multiple replicated services
- `update`: Updates a service

Creating a service:
```
docker service create -d --name [NAME] \
-p [HOST_PORT]:[CONTAINER_PORT] \
--replicas [REPLICAS] \
[IMAGE] [CMD]
```

List services:
```
docker service ls
```

Inspecting a service:
```
docker service inspect [NAME]
```

Get logs for a service:
```
docker service logs [NAME]
```

List all tasks of a service:
```
docker service ps [NAME]
```

Scale a service up or down:
```
docker service scale [NAME]=[REPLICAS]
```

Update a service:
```
docker service update [OPTIONS] [NAME]
```

Create nginx_service:
```
docker service create -d --name nginx_service -p 8080:80 --replicas 2 nginx:latest
```

List the swarm services:
```
docker service ls
```

Inspect nginx_service:
```
docker service inspect nginx_service
```

Find the network:
```
docker network ls --no-trunc | grep [NETOWRK_ID]
```

View the running tasks for nginx_service:
```
docker service ps nginx_service
```

Scale nginx_service to 3 replicas:
```
docker service scale nginx_service=3
```
