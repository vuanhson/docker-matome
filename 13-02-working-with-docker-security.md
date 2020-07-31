# Working with docker security

In this lesson we will start implementing some of the Docker security practices.

## Seccomp Profile
```
docker container run --security-opt seccomp=[PROFILE] [IMAGE] [CMD]
```

Testing Seccomp:
```
docker container run --rm -it alpine sh
whoami
mount /dev/sda1 /tmp
swapoff -a
```

Using a custom Seccomp profile:
```
mkdir -p seccomp/profiles/chmod
cd seccomp/profiles/chmod
wget https://raw.githubusercontent.com/moby/moby/master/profiles/seccomp/default.json
```

Remove `chmod`, `fchmod` and `fchmodat` from the syscalls whitelist. Syscalls starts at line 52.

Applying the custom Seccomp profile:
```
docker container run --rm -it --security-opt seccomp=./default.json alpine sh
chmod +r /usr
```

## Capabilities:
Dropping Capabilities:
```
docker container run --cap-drop=[CAPABILITY] [IMAGE] [CMD]
```

Test mknod:
```
docker container run --rm -it alpine sh
mknod /dev/random2 c 1 8
```

Disable mknod:
```
docker container run --rm -it --cap-drop=MKNOD alpine sh
mknod /dev/random2 c 1 8
```

Runtime privilege and Linux capabilities: https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities

## Control Groups
Limiting CPU and memory:
```
docker container run -it --cpus=[VALUE] --memory=[VALUE][SIZE] --memory-swap [VALUE][SIZE] [IMAGE] [CMD]
```

Setting memory limits on a container:
```
docker container run -d --name resource-limits --cpus=".5" --memory=512M --memory-swap=1G rivethead42/weather-app
```

Inspect resource-limits:
```
docker container inspect resource-limits
```

Runtime constraints on resources: https://docs.docker.com/engine/reference/run/#runtime-constraints-on-resources

More info on resource constraints: https://docs.docker.com/config/containers/resource_constraints/

## Running Docker Bench for Security
Running Docker Bench Security:
```
docker container run --rm -it --network host --pid host --userns host --cap-add audit_control \
    -e DOCKER_CONTENT_TRUST=$DOCKER_CONTENT_TRUST \
    -v /var/lib:/var/lib \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /usr/lib/systemd:/usr/lib/systemd \
    -v /etc:/etc --label docker_bench_security \
    docker/docker-bench-security
```
Docker Bench Security: https://github.com/docker/docker-bench-security

