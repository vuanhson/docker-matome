# Creating a compose file

In this lesson we will look at the basics of creating a compose file.

Setup your environment:
```
cd compose
git clone https://github.com/linuxacademy/content-weather-app.git weather-app
cd weather-app
git checkout compose
```

Create a docker-compose.yml file:
```
vi docker-compose.yml
```

docker-compose.yml contents:
```
version: '3'
services:
  weather-app:
    build:
      context: .
      args:
        - VERSION=v2.0
    ports:
      - "8081:3000"
    environment:
      - NODE_ENV=production
```

Create the compose container:
```
docker-compose up -d
```

List compose services:
```
docker-compose ps
```

Verify the weather-app is working:
```
curl http://localhost:8081
```

Rebuild the image:
```
docker-compose build
```

Rebuild the image with no cache:
```
docker-compose build --no-cache
```
