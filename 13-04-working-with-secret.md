# Working with secret

In this lesson, we will start working with Docker Secrets to protect sensitive data, such as passwords and API Keys.

Docker secrets commands:
- `create`: Create a secret from a file or STDIN as content
- `inspect`: Display detailed information on one or more secrets
- `ls`: List secrets
- `rm`: Remove one or more secrets

Creating a secret:
```
STDIN | docker secret create [NAME] -
```

List secrets:
```
docker secret ls
```

Inspecting a secret:
```
docker secret inspect [NAME]
```

Using secrets:
```
docker service create --name [NAME] --secret [SECERT] [IMAGE]
```

Deleting a secret:
```
docker secret rm [NAME]
```

Setup environment:
```
mkdir Secrets
cd secrets
```

Create a secret using STDIN:
```
openssl rand -base64 20 | docker secret create my_secret_data -
```

Create a secret using a file:
```
openssl rand -base64 20 > secret.txt
docker secret create my_secret_data2 secret.txt
```

Create a service using a secret:
```
docker service create --name redis --secret my_secret_data redis:alpine
```

Find the node the service is running on:
```
docker service ps redis
```

Remove secret my_secret_data2:
```
docker secret rm my_secret_data2
```

Generate password files:
```
openssl rand -base64 20 > db_password.txt
openssl rand -base64 20 > db_root_password.txt
```

Create a Wordpress Stack:
```
vi docker-compose.yml
```

docker-compose.yml contents:
```
version: '3.1'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     networks:
       mysql_internal:
         aliases: ["db"]
     environment:
       MYSQL_ROOT_PASSWORD_FILE: /run/secrets/db_root_password
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD_FILE: /run/secrets/db_password
     secrets:
       - db_root_password
       - db_password

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     networks:
       mysql_internal:
         aliases: ["wordpress"]
       wordpress_public:
     ports:
       - "8001:80"
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD_FILE: /run/secrets/db_password
     secrets:
       - db_password

secrets:
   db_password:
     file: db_password.txt
   db_root_password:
     file: db_root_password.txt

volumes:
    db_data:
networks:
  mysql_internal:
    driver: "overlay"
    internal: true
  wordpress_public:
    driver: "overlay"
```

Deploy stack:
```
docker stack deploy --compose-file docker-compose.yml wp
```