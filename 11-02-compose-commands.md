# Compose commands

In this lesson, we will start using compose by creating a compose file. Then we will create and manage the services by using the most commonly used commands:

- `build`: Build or rebuild services
- `bundle`: Generate a Docker bundle from the Compose file
- `config`: Validate and view the Compose file
- `create`: Create services
- `down`: Stop and remove containers, networks, images, and volumes
- `events`: Receive real time events from containers
- `exec`: Execute a command in a running container
- `help`: Get help on a command
- `images`: List images
- `kill`: Kill containers
- `logs`: View output from containers
- `pause`: Pause services
- `port`: Print the public port for a port binding
- `ps`: List containers
- `pull`: Pull service images
- `push`: Push service images
- `restart`: Restart services
- `rm`: Remove stopped containers
- `run`: Run a one-off command
- `scale`: Set number of containers for a service
- `start`: Start services
- `stop`: Stop services
- `top`: Display the running processes
- `unpause`: Unpause services
- `up`: Create and start containers
- `version`: Show the Docker-Compose version information

Setup your environment:
```
mkdir -p compose/commands
cd compose/commands
```

Create a docker-compose file:
```
vi docker-compose.yml
```

docker-compose.yml contents:
```
version: '3'
services:
  web:
    image: nginx
    ports:
    - "8080:80"
    volumes:
    - nginx_html:/usr/share/nginx/html/
    links:
    - redis
  redis:
    image: redis
volumes:
  nginx_html: {}
```

Create a compose service:
```
docker-compose up -d
```

List containers created by compose:
```
docker-compose ps
```

Stopping a compose service:
```
docker-compose stop
```

Starting a compose service:
```
docker-compose start
```

Restarting a compose service:
```
docker-compose restart
```

Delete a compose service:
```
docker-compose down
```