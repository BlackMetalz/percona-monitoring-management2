- Create instance from docker compose: https://github.com/moovs/pmm-in-docker-compose

- Change pass:

```
docker exec -t pmm-server bash -c  'ln -s /srv/grafana /usr/share/grafana/data; grafana-cli --homepath /usr/share/grafana admin reset-admin-password newpass'
```
