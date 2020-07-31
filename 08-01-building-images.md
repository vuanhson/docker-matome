# Building images

In this lesson, we will learn some alternate ways of building images.

To build one:
```
docker image build -t <NAME>:<TAG> .
```

Useful flags:

- `-f, --file` string: This is the name of the Dockerfile (Default is `PATH/Dockerfile`).
- `--force-rm`: Always remove intermediate containers.
- `--label` list: Set metadata for an image.
- `--rm`: Remove intermediate containers after a successful build (default is `true`).
- `--ulimit ulimit`: This sets `ulimit` options (default is []).

```
cd docker_images/weather-app
cp Dockerfile Dockerfile.test
docker image build -t linuxacademy/weather-app:path-example1 -f Dockerfile.test .
docker image build -t linuxacademy/weather-app:path-example2 --label com.linuxacademy.version=v1.8 -f Dockerfile.test .
```

Building image by piping the Dockerfile through STDIN:
```
docker image build -t <NAME>:<TAG> -<<EOF
Build instructions
EOF
```

Example:
```
docker image build -t linuxacademy/nginx:stind --rm -<<EOF
FROM nginx:latest
VOLUME ["/usr/share/nginx/html/"]
EOF
```

Building an image using a URL:
```
docker image build -t <NAME>:<TAG> <GIT_URL>#<REF>
docker image build -t <NAME>:<TAG> <GIT_URL>#:<DIRECTORY>
docker image build -t <NAME>:<TAG> <GIT_URL>#<REF>:<DIRECTORY>
```

Example:
```
docker image build -t linuxacademy/weather-app:github https://github.com/linuxacademy/content-weather-app.git#remote-build
```

Building an image from a zip file:
```
docker image build -t <NAME>:<TAG> - < <FILE>.tar.gz
```

Example:
```
cd docker_images
mkdir tar_image
cd tar_image
git clone https://github.com/linuxacademy/content-weather-app.git
cd content-weather-app
git checkout remote-build
tar -zcvf weather-app.tar.gz Dockerfile src
docker image build -t linuxacademy/weather-app:from-tar - < weather-app.tar.gz
```