# Docker logging

In this lesson, you will learn how to view the logs of a container to get vital output of your application. You will also learn about some of the logging best practices of containerized applications.

Create a container using the weather-app image.
```
docker container run --name weather-app -d -p 80:3000 linuxacademycontent/weather-app
```

Show information logged by a running container:
```
docker container logs [NAME]
```

Show information logged by all containers participating in a service:
```
docker service logs [SERVICE]
```

Logs need to be output to `STDOUT` and `STDERR`.

Nginx Example:
```
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log
```

Debug a failed container deploy:
```
docker container run -d --name ghost_blog \
-e database__client=mysql \
-e database__connection__host=mysql \
-e database__connection__user=root \
-e database__connection__password=P4sSw0rd0! \
-e database__connection__database=ghost \
-p 8080:2368 \
ghost:1-alpine
```

Useful links:
- [12 Factor Logs](https://12factor.net/logs)
- [Weather App Code](https://github.com/linuxacademy/content-intermediate-docker-quest/tree/logging)
- [Ruby Logging](https://ruby-doc.org/stdlib-2.6/libdoc/logger/rdoc/Logger.html)
- [Python Logging](https://docs.python.org/2/howto/logging.html)
