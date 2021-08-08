
# High Availability (alerting) with Alertmanager

## Summary

| Service      |         |                       |
|:-------------|---------|-----------------------|
| Alertmanager | am-01   | http://localhost:9091 |
| Alertmanager | am-02   | http://localhost:9092 |
| Alertmanager | am-03   | http://localhost:9093 |
| Prometheus   | prom-01 |                       |
| Prometheus   | prom-02 |                       |

Prometheus UI ports are not exposed intentionally as this example is intended only for alerting. Grafana in not present for the same reason.

## Description

This example is composed of a cluster with 3x AlertManager instances and 2x Prometheus with duplicated configurations to evaluate and send alerts reliably.

To validate if the Alermanager cluster is running create a *Silence* and all Alertmanager instances will received it. Tweak the value of *--cluster.pushpull-interval=5s* for Alertmanager instances in *docker-compose.yaml* as required.

Both Prometheus instances are configured to scrape the Alertmanagers and Prometheus hosts and have a duplicated setup (the same file is used as configuration for both Prometheus).

An alert is set in [prometheus/alerts.yaml](prometheus/alerts.yaml) to be triggered when a prometheus or alertmanager instance goes down. To test stop one or more instances. 

Alertmanager will deduplicate the alerts from both prometheus and only one of the Alertmanagers will send the alert.

Slack or other supported messaging can be set to receive alerts at [alertmanager/config.yaml](alertmanager/config.yaml).

## Conclusion

This setup will work well for alerting purposes unless you have a very large number of rules to be evaluated. If/When that happens you can try to vertically scale Prometheus by adding more ram and optimize the alert expressions (hint: use a linter) with recording rules.
