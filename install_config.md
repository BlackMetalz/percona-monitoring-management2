Credit:
- https://github.com/moovs/pmm-in-docker-compose
- https://www.percona.com/doc/percona-monitoring-and-management/2.x/install/docker.html
- https://www.percona.com/blog/2019/09/19/installing-percona-monitoring-and-management-pmm-2-for-the-first-time/

- 1. Install The Server

- 1.1: Create mysql user for ppm


- 2. Instal The Agent

- 3. Config
```
pmm-admin config --server-insecure-tls --server-url=https://admin:admin@<IP
˓ → Address>:443
```

- Output:
```
Checking local pmm-agent status...
pmm-agent is running.
Registering pmm-agent on PMM Server...
Registered.
Configuration file /usr/local/percona/pmm2/config/pmm-agent.yaml updated.
Reloading pmm-agent configuration...
Configuration reloaded.
Checking local pmm-agent status...
pmm-agent is running.
```

- Adding MySQL Metrics and Query Analytics
+ Permission required:
```
CREATE USER 'pmm'@'127.0.0.1' IDENTIFIED BY 'pass' WITH MAX_USER_CONNECTIONS 10;
GRANT SELECT, PROCESS, SUPER, REPLICATION CLIENT, RELOAD ON *.* TO 'pmm'@'127.0.0.1';
```
+ Add service:
```
pmm-admin add mysql --query-source=perfschema --username=pmm --password=pass
```
+ More detail:
```
pmm-admin add mysql --username=pmm --password=pmm --query-source=perfschema ps-mysql 127.0.0.1:3306
```

+ Also available in socket linux:
```
pmm-admin add mysql --socket=/var/path/to/mysql/socket
```

+ Table statistics collection disabled (the limit is 1000, the actual table count is 2469).
```

pmm-admin add mysql --query-source=perfschema --username=pmm --password=pass --disable-tablestats
```


