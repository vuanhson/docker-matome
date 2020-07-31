# Saving and Loading images

In this lesson, we will learn how to save an image to a tar file, and see how to load it back in.

Save one or more images to a tar file:
```
docker image save <IMAGE> > <FILE>.tar
docker image save <IMAGE> -o <FILE>.tar
docker image save <IMAGE> --output <FILE>.tar
```

Load an image from a tar file:
```
docker image load < <FILE>.tar
docker image load -i <FILE>.tar
docker image load --input <FILE>.tar
```

Setup:
```
mkdir output
cd output
```

Archive the rivethead42/weather-app:latest image:
```
docker image save rivethead42/weather-app:latest --output weather-app-latest.tar
```

Inspect the tar file:
```
tar tvf weather-app-latest.tar
```

Compress the tar file:
```
gzip weather-app-latest.tar
```

Delete the image:
```
docker image rm [USERNAME]/weather-app:latest
```

Load the weather-app image from a tar file:
```
docker image load --input weather-app-latest.tar.gz
docker image ls | grep [USERNAME]/weather-app
docker image rm rivethead42/weather-app:latest docker image ls | grep rivethead42/weather-app
```