# Using network in swarm mode

In this lesson, we'll look more into overlay networks and how they are used with a swarm.

Create a overlay network:
```
docker network create -d overlay [NAME]
```

Creating a service with an overlay network:
```
docker service create -d --name [NAME] \
--network [NETWORK] \
-p [HOST_PORT]:[CONTAINER_PORT] \
--replicas [REPLICAS] \
[IMAGE] [CMD]
```

Add a service to a network:
```
docker service update --network-add [NETWORK] [SERVICE]
```

Remove a service from a network:
```
docker service update --network-rm [NETWORK] [SERVICE]
```

Create a overlay network:
```
docker network create -d overlay my_overlay
```

Create an encrypted overlay network:
```
docker network create -d overlay --opt encrypted encrypted_overlay
```

Inspect encrypted_overlay:
```
docker network inspect encrypted_overlay
```

Inspect my_overlay:
```
docker network inspect my_overlay
```

Create a service using my_overlay:
```
docker service create -d --name nginx_overlay  --network my_overlay -p 8081:80 --replicas 2 nginx:latest
```

Adding the my_overlay network to nginx_service:
```
docker service update --network-add my_overlay nginx_service
```

Inspect nginx_service:
```
docker service inspect nginx_service
```

Removing the ingress network from nginx_service:
```
docker service update --network-rm my_overlay nginx_service
```

Inspect nginx_service:
```
docker service inspect nginx_service
```

Remove encrypted_overlay:
```
docker network rm encrypted_overlay
```