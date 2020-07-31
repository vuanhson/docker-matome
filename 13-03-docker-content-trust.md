# Docker content trust

In this lesson you will learn how to sign images and enable Docker Content Trust to ensure that the images you are pulling have been verified.

## Commands
Creating a Key:
```
docker trust key generate [NAME]
```

Importing a Key:
```
docker trust key load [PEM] --name [NAME]
```

Add a signer:
```
docker trust signer add --key [PEM] [NAME] [REPOSITORY]
```

Remove a signer:
```
docker trust signer remove [NAME] [REPOSITORY]
```

Signing an image:
```
docker trust sign [IMAGE]:[TAG]
```

## Using DCT to sign an image
Tag the image that will be signed:
```
docker image tag [USERNAME]/weather-app:latest [USERNAME]/dct:latest
```

Create a Key:
```
docker trust key generate [NAME]
```

Add your signer user:
```
docker trust signer add --key [NAME].pub [NAME] [USERNAME]/dct
```

Sign and push your image to Docker Hub:
```
docker trust sign [USERNAME]/dct:latest
export DOCKER_CONTENT_TRUST=1
docker image push [USERNAME]/dct:latest
```

Remove the Docker image [USERNAME]/weather-app:
```
docker image rm [USERNAME]/weather-app:latest
```

Pull [USERNAME]/weather-app:
```
docker image pull [USERNAME]/weather-app
```

Remove the Nginx image:
```
docker image rm nginx:latest
```

Pull the image:
```
docker image pull nginx:latest
```

Enabling DCT
```
vi /etc/docker/daemon.json
```

/etc/docker/daemon.json:
```
{
    "content-trust": {
        "mode": "enforced"
    }
}
```
