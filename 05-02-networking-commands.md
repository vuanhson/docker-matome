# Networking commands

## Networking Basics
```
ifconfig
```

List all Docker network commands:
```
docker network -h
```

- `connect` Connect a container to a network 
- `create` Create a network 
- `disconnect` Disconnect a container from a network 
- `inspect` Display detailed information on one or more networks 
- `ls` List networks 
- `prune` Remove all unused networks 
- `rm` Remove one or more networks

List all Docker networks on the host:
```
docker network ls
docker network ls --no-trunc
```

Getting detailed info on a network:
```
docker network inspect [NAME]
```

Creating a network:
```
docker network create br00
```

Deleting a network:
```
docker network rm [NAME]
```
Warning: do not delete default networks

Remove all unused networks:
```
docker network prune
```

## Adding and Removing containers to a network
Create a container with no network:
```
docker container run -d --name network-test03 -p 8081:80 nginx
```

Create a new network:
```
docker network create br01
```

Add the container to the bridge network:
```
docker network connect br01 network-test03
```

Inspect network-test03 to see the networks:
```
docker container inspect network-test03
```

Remove network-test03 from br01:
```
docker network disconnect br01 network-test03
```

