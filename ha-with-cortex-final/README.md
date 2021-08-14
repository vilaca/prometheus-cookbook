# cortexproject/cortex docker-compose

 > use haproxy for loadblance

## how to running

* start docker-compose services

```code

docker-compose up -d
```

* view ring

```code
open http://localhost:9001/ring
```

* viw prometheus console

```code
open http://localhost:9090
```

* view grafana  ui

> note:  you need add prometheus datasource

```code

open http://localhost:3000
```

* add dashboard json file

```code
1-node-exporter-0-16-for-prometheus_rev9.json 

or 
1-node-exporter-0-16-for-prometheus-monitoring-display-board_rev1.json

```