# Installing docker compose

In this lesson, we will learn about installing Docker Compose and why we should use it.

Download the latest version of Docker Compose:
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Apply executable permissions:
```
sudo chmod +x /usr/local/bin/docker-compose
```

Test Docker Compose:
```
docker-compose --version
```

Declare your entire (microservice) application in a single YAML file, take that file to deploy your application and manage lifecycle of it.