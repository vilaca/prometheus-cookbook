
# High availability Alertmanager

3x AlertManager instances and 2x Prometheus instances to evaluate alerts.

Alertmanager will deduplicate the alerts from both prometheus and only one of the Alertmanagers will send the alert.

TSDB storage is set to 3h

This setup will work well for alerting purposes unless you have a very large number of rules to be evaluated. If/When that happens you can try to vertically scale Prometheus by adding more ram and optimize the alert expressions (hint: use a linter) with recording rules. If that fails split your rules set across more than one instance.

| Service      |         |                        |
|--------------|:--------|------------------------|
| Alertmanager | am-01   | http://localhost:9091/ |
| Alertmanager | am-02   | http://localhost:9092/ |
| Alertmanager | am-03   | http://localhost:9093/ |
| Prometheus   | prom-01 |                        |
| Prometheus   | prom-02 |                        |

Prometheus UI port is not exposed intentionally as this example is intended only for alerting.
