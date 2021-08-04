
# High availability with Thanos



| Service        |                  |                        |
|----------------|:-----------------|------------------------|
| Alertmanager   | am-01            | http://localhost:8101/ |
| Prometheus     | prom-01          | http://localhost:8201/ |
| Prometheus     | prom-02          | http://localhost:8202/ |
| Thanos sidecar | prom-01-sidecar  |                        |
| Thanos sidecar | prom-02-sidecar  |                        |
| Thanos query   | querier-01       | http://localhost:8401/ |
| Thanos store   | store-gateway-01 | http://localhost:8501/ |
| Minio          | minio-01         | http://localhost:9000 |
| Grafana        | grafana-01       | http://localhost:8301/ |



