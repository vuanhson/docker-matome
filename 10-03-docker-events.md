# Docker events

In this lesson, we'll see how to listen for events using the events command.

Get real-time events from the server:
```
docker system events
docker system events --since '<TIME_PERIOD>'
```

Start a new CentOS container:
```
docker container run -itd --name docker_events centos /bin/bash
```

Listen for events:
```
docker system events
```

Generate Events:
```
docker container exec docker_events /bin/bash
docker container attach docker_events
docker container start docker_events
```

Filters Events:
```
docker system events --filter <FILTER_NAME>=<FILTER>
```

Filter for container events:
```
docker system events --filter type=container --since '1h'
```

Generate an event:
```
docker container exec docker_events ls /
```

Filter for container events:
```
docker system events --filter type=container --filter event=start --since '1h'
```

List / on docker_events:
```
docker container exec docker_events ls /
```

Filter for attach events:
```
docker system events --filter type=container --filter event=attach
```

Connect to docker_events using /bin/bash:
```
docker container exec -it docker_events /bin/bash
```

Attach to docker_events:
```
docker container attach docker_events
```

Connect to docker_events using /bin/bash:
```
docker container exec -it docker_events /bin/bash
```

Attach to docker_events:
```
docker container attach docker_events
```

Use multiple filters:
```
docker system events --filter type=container --filter event=attach --filter event=die --filter event=stop
```

Start docker_events:
```
docker container start docker_events
```

Attach to docker_events:
```
docker container attach docker_events
```

Documentation:

docker events: https://docs.docker.com/engine/reference/commandline/events/
Engine API v1.24: https://docs.docker.com/engine/api/v1.24/

