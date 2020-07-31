# Updating containers with watch tower

In this lesson, we'll see how to use Watchtower to keep a container up-to-date when its image gets updated.

Clone Express app:
```
git clone https://github.com/linuxacademy/content-express-demo-app.git watchtower
cd watchtower
git checkout dockerfile
```

Build the Docker image:
```
docker login -u [USERNAME]
docker image build -t rivethead42/my-express .
docker image push rivethead42/my-express
```

Create the container:
```
docker container run -d --name watched-app -p 80:3000 --restart always rivethead42/my-express
```

Create Watchtower:
```
docker container run -d --name watchtower \
--restart always \
-v /var/run/docker.sock:/var/run/docker.sock \
v2tec/watchtower -i 15
```

Add a .dockerignore file:
```
vi .dockerignore
```

.dockerignore contents:
```
Dockerfile
.git
.gitignore
```

Edit app.js and add a comment:
```
vi app.js
```

app.js contents:
```
//This is a comment
//
...
```

Add the file newfile.js:
```
touch newfile.js
```

Rebuild the image:
```
docker image build -t rivethead42/my-express --no-cache .
docker image push rivethead42/my-express
```

Check to see if the container was restarted with the new image:
```
docker container ls
```

Verify the changes by attaching to watched-app:
```
docker container exec -it watched-app /bin/bash
```