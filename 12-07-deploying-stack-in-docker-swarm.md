# Deploying Stack in Docker Swarm

Deploying Stacks in Docker Swarm
In this lesson, we will learn how to deploy stacks to Docker Swarm using Docker Compose.

Docker stack commands:
- `deploy`: Deploys a new stack or update an existing stack
- `ls`: Lists stacks
- `ps`: Lists the tasks in the stack
- `rm`: Removes one or more stacks
- `services`: Lists the services in the stack

Setup environment:
```
mkdir -p swarm/prometheus
cd swarm/prometheus
```

Create the prometheus.yml file:
```
vi prometheus.yml
```

prometheus.yml contents:
```
global:
  scrape_interval: 15s
  scrape_timeout: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: prometheus
    scrape_interval: 5s
    static_configs:
    - targets:
      - prometheus_main:9090

  - job_name: nodes
    scrape_interval: 5s
    static_configs:
    - targets:
      - [MANAGER]:9100
      - [WORKER1]:9100
      - [WORKER2]:9100

  - job_name: cadvisor
    scrape_interval: 5s
    static_configs:
    - targets:
      - [MANAGER]:8081
      - [WORKER1]:8081
      - [WORKER2]:8081
```

Create a compose file:
```
vi docker-compose.yml
```

docker-compose.yml contents:
```
version: '3'
services:
  main:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
      - 8080:9090
    command:
      - --config.file=/etc/prometheus/prometheus.yml
      - --storage.tsdb.path=/prometheus/data
    volumes:
    - ./prometheus.yml:/etc/prometheus/prometheus.yml:ro
    - data:/prometheus/data
    depends_on:
      - cadvisor
      - node-exporter
  cadvisor:
    image: google/cadvisor:latest
    container_name: cadvisor
    deploy:
      mode: global
    restart: unless-stopped
    ports:
      - 8081:8080
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:rw
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    deploy:
      mode: global
    restart: unless-stopped
    ports:
      - 9100:9100
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.sysfs=/host/sys'
      - --collector.filesystem.ignored-mount-points
      - "^/(sys|proc|dev|host|etc|rootfs/var/lib/docker/containers|rootfs/var/lib/docker/overlay2|rootfs/run/docker/netns|rootfs/var/lib/docker/aufs)($$|/)"
  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - 8082:3000
    volumes:
    - grafana_data:/var/lib/grafana
    - grafana_plugins:/var/lib/grafana/plugins
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=P4ssW0rd0!
    depends_on:
      - prometheus
      - cadvisor
      - node-exporter

volumes:
  data:
  grafana_data:
  grafana_plugins:
```

Deploy the stack:
```
docker stack deploy --compose-file docker-compose.yml prometheus
```

List stacks:
```
docker stack ls
```

List services:
```
docker service ls
```

Fix volume permissions:
```
sudo chown nfsnobody:nfsnobody -R /var/lib/docker/volumes/prometheus_data
```
