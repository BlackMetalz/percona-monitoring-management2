# Create instance from docker compose: https://github.com/moovs/pmm-in-docker-compose
- Detai:
+ Create pmm-data container:
```
docker create \
   -v /opt/prometheus/data \
   -v /opt/consul-data \
   -v /var/lib/mysql \
   -v /var/lib/grafana \
   --name pmm-data \
   percona/pmm-server:2 /bin/true
```
+ the second step is create and start pmm-server container to initialize the data directory correctly
```
docker run -d \
  -p 80:80 \
  --volumes-from pmm-data \
  --name pmm-server \
  --restart always \
  percona/pmm-server:2

```
+ Stop and remove pmm-server container:
```
docker stop pmm-server && docker rm pmm-server

```

+ Create folder for pmm-server data:
```
mkdir -p /data/pmm2-server/
```

+ Copy data
```
docker cp pmm-data:/opt/prometheus/ /data/pmm2-server/
docker cp pmm-data:/opt/consul-data/ /data/pmm2-server/
docker cp pmm-data:/var/lib/mysql/ /data/pmm2-server/
docker cp pmm-data:/var/lib/grafana/ /data/pmm2-server/
```
+ docker-compose.yml
```
version: '2'

services:
  pmm-data:
    image: percona/pmm-server:2
    container_name: pmm-data
    volumes:
      - /data/pmm2-server/prometheus/data:/opt/prometheus/data
      - /data/pmm2-server/consul-data:/opt/consul-data
      - /data/pmm2-server/mysql:/var/lib/mysql
      - /data/pmm2-server/grafana:/var/lib/grafana
    entrypoint: /bin/true

  pmm-server:
    image: percona/pmm-server:2
    container_name: pmm-server
    ports:
      - '80:80'
      - '443:443'
    restart: always
    volumes_from:
      - pmm-data
```


# Change pass:

```
docker exec -t pmm-server bash -c  'ln -s /srv/grafana /usr/share/grafana/data; grafana-cli --homepath /usr/share/grafana admin reset-admin-password newpass'
```
