# Networking containers

In this lesson, we will dig deeper into container networking by supplying our own subnet and gateway when creating a new network. We will then move on to networking two different containers using an internal network. This will allow one container to be publicly accessible while the other one is not.

## Creating a network and defining a Subnet and Gateway
Create a bridge network with a subnet and gateway:
```
docker network create --subnet 10.1.0.0/24 --gateway 10.1.0.1 br02
```

Run ifconfig to view the bridge interface for br02:
```
ifconfig
```
Created interface name format: `bridge-<networkid>`, eg. br-6f3630f5e4ae


Inspect the `br02` network:
```
docker network inspect br02
```

Prune all unused networks:
```
docker network prune
```
`prune` will NOT delete default networks


Create a network with an IP range:
```
docker network create --subnet 10.1.0.0/16 --gateway 10.1.0.1 \
--ip-range=10.1.4.0/24 --driver=bridge --label=host4network br04
```

Inspect the `br04` network:
```
docker network inspect br04
```

Create a container using the br04 network:
```
docker container run --name network-test01 -it --network br04 centos /bin/bash
```

Install Net Tools:
```
yum update -y
yum install -y net-tools
```

Get the IP info for the container:
```
ifconfig
```

Get the gateway info the container:
```
netstat -rn
```

Get the DNS info for the container:
```
cat /etc/resolv.conf
```

## Assigning IPs to a container:
Create a new container and assign an IP to it:
```
docker container run -d --name network-test02 --ip 10.1.4.102 --network br04 nginx
```

Get the IP info for the container:
```
docker container inspect network-test02 | grep IPAddr
```

Inspect network-test03 to see that br01 was removed:
```
docker container inspect network-test04
```

## Networking two containers
Create an internal network: (Not bound to any interface)
```
docker network create -d bridge --internal localhost
```

Create a MySQL container that is connected to localhost:
```
docker container run -d --name test_mysql \
-e MYSQL_ROOT_PASSWORD=P4sSw0rd0 \
--network localhost mysql:5.7
```

Create a container that can ping the MySQL container:
```
docker container run -it --name ping-mysql \
--network bridge \
centos
```

Connect ping-mysql to the localhost network:
```
docker network connect localhost ping-mysql
```

Restart and attach to container:
```
docker container start -ia ping-mysql
```

Create a container that can't ping the MySQL container:
```
docker container run -it --name cant-ping-mysql \
centos
```

Create a Nginx container that is not publicly accessible:
```
docker container run -d --name private-nginx -p 8081:80 --network localhost nginx
```

Inspect private-nginx:
```
docker container inspect private-nginx
```
