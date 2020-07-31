# Use volume for persistent storage

In this lesson, we will take a deeper look into using volumes with our Docker containers. Volumes are the preferred method for maintaining persistent data.

Volumes are easier to back up or migrate than bind mounts. You can manage volumes using Docker CLI commands or the Docker API. They work on both Linux and Windows containers. Volumes can be more safely shared among multiple containers. Volume drivers allow for:
- Storing volumes on remote hosts or cloud providers
- Encrypting the contents of volumes
- Add other functionality

New volumes can have their content pre-populated by a container.

Create a new volume for an Nginx container:
```
docker volume create html-volume
```

Creating a volume using that volume mount:
```
docker container run -d \
 --name nginx-volume1 \
 --mount type=volume,source=html-volume,target=/usr/share/nginx/html/ \
 nginx
```

Inspect the volume:
```
docker volume inspect html-volume
```

List the contents of html-volume:
```
sudo ls /var/lib/docker/volumes/html-volume/_data
```

Creating a volume using that volume flag:
```
docker container run -d \
 --name nginx-volume2 \
 -v html-volume:/usr/share/nginx/html/ \
 nginx
```

Edit index.html:
```
sudo vi /var/lib/docker/volumes/html-volume/_data/index.html
```

Inspect nginx-volume2 to get the private IP:
```
docker container inspect nginx-volume2
```

Login into nginx-volume1 and go to the html directory:
```
docker container exec -it nginx-volume1 /bin/bash
cd /usr/share/nginx/html
cat index.hml
```

Install Vim:
```
apt-get update -y
apt-get install vim -y
```

Using a readonly volume:
```
docker run -d \
  --name=nginx-volume3 \
  --mount source=html-volume,target=/usr/share/nginx/html,readonly \
  nginx
```

Login into nginx-volume3 and go to the html directory:
```
docker container exec -it nginx-volume3 /bin/bash
cd /usr/share/nginx/html
cat index.hml
```

Install Vim:
```
apt-get update -y
apt-get install vim -y
```
