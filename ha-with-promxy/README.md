
# High Availability Prometheus with Promxy

| Service      |              |                        |
|--------------|:-------------|------------------------|
| am-01        | Alertmanager | http://localhost:8101/ |
| am-02        | Alertmanager | http://localhost:8102/ |
| am-03        | Alertmanager | http://localhost:8103/ |
| prom-01      | Prometheus   | http://localhost:8201/ |
| prom-02      | Prometheus   | http://localhost:8202/ |
| promxy-01    | Promxy       | http://localhost:8801/ |

## Summary

Prometheus is a single process application not capable of running in a cluster by itself.

[Promxy](https://github.com/jacksontj/promxy) merges data from duplicate Prometheus hosts and provides a single datasource for Grafana.

Promxy works by querying all Prometheus in a server group, merging the responses into a single response for Grafana. Gaps can still exist if not one of the duplicated Prometheus instances has samples for a time period. 

In this example both Prometheus instances are configured to scrape themselves and the Alertmanagers. They share the same configuration files meaning they're _duplicated_.

To validate that the cluster is running create a *Silence* and all Alertmanager instances should see it. Tweak the value of *--cluster.pushpull-interval=5s* for Alertmanager instances in *docker-compose.yaml* as required.

An alert is set in [prometheus/alerts.yaml](prometheus/alerts.yaml) to be triggered when a prometheus or alertmanager instance goes down. To test the alert stop one or more instances. 

Alertmanager will deduplicate the alerts from both prometheus and only one of the Alertmanagers will send the alert.

Slack or other supported messaging can be set to receive alerts at [alertmanager/config.yaml](alertmanager/config.yaml).
