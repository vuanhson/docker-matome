# Using bind mounts

Bind mounts have been around since the early days of Docker. They have limited functionality compared to volumes. With bind mount, a file or directory on the host machine is mounted into a container.

Volumes use a new directory that is created within Docker’s storage directory on the host machine, and Docker manages that directory’s contents.

Using the mount flag:
```
mkdir target

docker container run -d \
  --name nginx-bind-mount1 \
  --mount type=bind,source="$(pwd)"/target,target=/app \
  nginx
```
```
docker container ls
```
Bind mounts won't show up when listing volumes:
```
docker volume ls
```

Inspect the container to find the bind mount:
```
docker container inspect nginx-bind-mount1
```

Create a new file in /app on the container:
```
docker container exec -it nginx-bind-mount1 /bin/bash
cd target
touch file1.txt
ls
exit
```

Using the volume flag:
```
docker container run -d \
 --name nginx-bind-mount2 \
 -v "$(pwd)"/target2:/app \
 nginx
```

Create /app/file3.txt in the container:

```
docker container exec -it nginx-bind-mount2 touch /app/file3.txt
ls target2
```

Create an nginx.conf file:
```
mkdir nginx
cat << EOF >  nginx/nginx.conf
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
EOF
```

Create an Nginx container that creates a bind mount to `nginx.conf`:
```
docker container run -d \
 --name nginx-bind-mount3 \
 -v "$(pwd)"/nginx/nginx.conf:/etc/nginx/nginx.conf \
 nginx
```

Look at the bind mount by inspecting the container:
```
docker container inspect nginx-bind-mount3
```

Originally, the -v or --volume flag was used for standalone containers and the --mount flag was used for swarm services. However, starting with Docker 17.06, you can also use --mount with standalone containers. In general, --mount is more explicit and verbose. The biggest difference is that the -v syntax combines all the options together in one field, while the --mount syntax separates them. Here is a comparison of the syntax for each flag.

Because the -v and --volume flags have been a part of Docker for a long time, their behavior cannot be changed. This means that there is one behavior that is different between -v and --mount.

If you use -v or --volume to bind-mount a file or directory that does not yet exist on the Docker host, -v creates the endpoint for you. It is always created as a directory.

If you use --mount to bind-mount a file or directory that does not yet exist on the Docker host, Docker does not automatically create it for you, but generates an error.

https://docs.docker.com/storage/bind-mounts/