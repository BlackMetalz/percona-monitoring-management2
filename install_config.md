Credit:
- https://github.com/moovs/pmm-in-docker-compose
- https://www.percona.com/doc/percona-monitoring-and-management/2.x/install/docker.html


1. Install The Server

1.1: Create mysql user for ppm


2. Instal The Agent

3. Config
```
pmm-admin config --server-insecure-tls --server-url=https://admin:admin@<IP
˓ → Address>:443
```

Output:
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

