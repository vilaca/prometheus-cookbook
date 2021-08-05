
# High availability Alertmanager

3x AlertManager instances and 2x Prometheus instances to evaluate and send alerts.

Both prometheus instances are configured to scrape themselves and the alertmanagers. They share the same configuration files.

In [prometheus/alerts.yaml](prometheus/alerts.yaml) an alert is configured to alert when a prometheus or alertmanager instance goes down. It can be tested by stopping on or more instances.

To validate if the cluster is running create a *Silence* and all Alertmanager instances should see it. Tweak the value of *--cluster.pushpull-interval=5s* for Alertmanager instances in *docker-compose.yaml* as required.

Alertmanager will deduplicate the alerts from both prometheus and only one of the Alertmanagers will send the alert.

This setup will work well for alerting purposes unless you have a very large number of rules to be evaluated. If/When that happens you can try to vertically scale Prometheus by adding more ram and optimize the alert expressions (hint: use a linter) with recording rules. If that fails split your rules set across more than one instance.

| Service      |         |                        |
|--------------|:--------|------------------------|
| Alertmanager | am-01   | http://localhost:9091/ |
| Alertmanager | am-02   | http://localhost:9092/ |
| Alertmanager | am-03   | http://localhost:9093/ |
| Prometheus   | prom-01 |                        |
| Prometheus   | prom-02 |                        |

Prometheus UI port is not exposed intentionally as this example is intended only for alerting.
