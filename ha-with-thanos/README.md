
# High availability with Thanos

3x AlertManager instances and 2x Prometheus instances to evaluate alerts.

Alertmanager will deduplicate the alerts from both prometheus and only one of the Alertmanagers will send the alert.

This setup will work well for alerting purposes unless you have a very large number of rules to be evaluated. If/When that happens you can try to vertically scale Prometheus by adding more ram and optimize the alert expressions (hint: use a linter) with recording rules. If that fails split your rules set across more than one instance.

| Service        |                  |                        |
|----------------|:-----------------|------------------------|
| Alertmanager   | am-01            | http://localhost:9091/ |
| Alertmanager   | am-02            | http://localhost:9092/ |
| Alertmanager   | am-03            | http://localhost:9093/ |
| Prometheus     | prom-01          | http://localhost:9081/ |
| Prometheus     | prom-02          | http://localhost:9082/ |
| Thanos sidecar | prom-01-sidecar  |                        |
| Thanos sidecar | prom-02-sidecar  |                        |
| Thanos query   | querier-01       | http://localhost:9082/ |
| Thanos store   | store-gateway-01 | http://localhost:9082/ |
| Minio          | minio-01         | http://localhost:9082/ |
| Grafana        | grafana-01       | http://localhost:9082/ |



