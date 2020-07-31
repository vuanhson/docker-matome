# Using volume in swarm mode

In this lesson we will start learning about plugins, and using volumes in swarm mode. The local driver only creates a volume on the node that a command is executed on. This requires using a third party driver that is specific to the environment.

Add Plugins:
```
docker plugin install [PLUGIN] [OPTIONS]
```

List plugins:
```
docker plugin ls
```

Volume Plugins:
```
Hedvig
Pure Storage
HPE Nimble Storage
Nutanix DVP
Blockbridge
NexentaStor
StorageOS
Rex-Ray
```

Install the Splunk plugin:
```
docker plugin install store/splunk/docker-logging-plugin:2.0.0 --alias splunk-logging-plugin
```

Disable a plugin:
```
docker plugin disable [ID]
```

Remove a plugin:
```
docker plugin rm [ID]
```

Digital Ocean example:
```
docker plugin install rexray/dobs \
DOBS_REGION=<DO_REGION> \
DOBS_TOKEN=<DIGITAL_OCEAN_TOKEN> \
DOBS_CONVERTUNDERSCORES=true
```

Create a volume using a driver:
```
docker volume create -d [DRIVER] [NAME]
```
```
docker service create -d --name [NAME] \
--mount type=[TYPE],src=[SOURCE],dst=[DESTINATION] \
-p [HOST_PORT]:[CONTAINER_PORT] \
--replicas [REPLICAS] \
[IMAGE] [CMD]
```

Create a volume on the manager:
```
docker volume create -d local portainer_data
```

Create a portainers service that uses a volume:
```
docker service create \
--name portainer \
--publish 8000:9000 \
--constraint 'node.role == manager' \
--mount type=volume,src=portainer_data,dst=/data \
--mount type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
portainer/portainer \
-H unix:///var/run/docker.sock
```

Volume Driver: https://hub.docker.com/search?q=volume%20plugins&type=plugin&category=volume

Rex-ray volume driver: https://rexray.readthedocs.io/en/stable/user-guide/schedulers/docker/plug-ins/