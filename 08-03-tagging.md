# Tagging
In this lesson, we will talk about how to use the tag command, and best practices to keep in mind when tagging.

Add a name and an optional tag with -t or --tag, in the name:tag format:
```
docker image build -t <name>:<tag>
docker image build --tag <name>:<tag>
```

List your images:
```
docker image ls
```

Use our Git commit hash as the image tag:
```
git log -1 --pretty=%H
```

Use the Docker tag to a create a new tagged image:
```
docker tag <SOURCE_IMAGE><:TAG> <TARGET_IMAGE>:<TAG>
```

Get the commit hash:
```
cd docker_images/weather-app/src
git log -1 --pretty=%H
cd ../
```

Build the image using the Git hash as the tag:
```
docker image build -t linuxacademy/weather-app:<GIT_HASH> .
```

Tag the weather-app as the latest using the image tagged with the commit hash:
```
docker image tag linuxacademy/weather-app:<GIT_HASH> linuxacademy/weather-app:latest
```