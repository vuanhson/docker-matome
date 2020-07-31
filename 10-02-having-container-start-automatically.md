# Having container start automatically

In this lesson, we will look at how to set restart policies for containers, and how that will effect their behavior when the docker service is restarted.

To configure the restart policy for a container, use the `--restart` flag:

- `no`: Do not automatically restart the container. (the default)
- `on-failure`: Restart the container if it exits due to an error, which manifests as a non-zero exit code.
- `always`: Always restart the container if it stops.
- `unless-stopped`: Similar to always, except that when the container is stopped, it is not restarted even after the Docker daemon restarts.

Automatically Restarting a container:
```
docker container run -d --name <NAME> --restart <RESTART> <IMAGE>
```

Make sure a container always restarts:
```
docker container run -d --name always-restart --restart always rivethead42/weather-app:latest
```

Make sure a container restarts unless it's stopped:
```
docker container run -d --name unless-stopped --restart unless-stopped rivethead42/weather-app:latest
```

Stop and restart your Docker service:
```
sudo systemctl restart docker
```

List your containers:
```
docker container ls
```

Stop the unless-stopped container:
```
docker container stop unless-stopped
```

Stop and restart your Docker service:
```
sudo systemctl restart docker
```

List your containers:
```
docker container ls
```

Stop the unless-stopped container:
```
docker container stop always-restart
```

Stop and restart your Docker service:
```
sudo systemctl restart docker
```

List your containers:
```
docker container ls
```