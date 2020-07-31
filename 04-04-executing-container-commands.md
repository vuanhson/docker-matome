# Executing container commands

In this lesson we'll see three different ways to execute commands on containers.

Executing a command:
- Dockerfile (future lession)
- During a Docker run
- Using the exec command

Commands can be:
- One and done Commands
- Long running Commands

Start a container with a command:
```
docker container run [IMAGE] [CMD]
```

Execute a command on a container:
```
docker container exec -it [NAME] [CMD]
```

Example:
```
docker container run -d -p 8080:80 nginx
docker container ps
docker container exec -it [NAME] /bin/bash
docker container exec -it [NAME] ls /usr/share/nginx/html/
```