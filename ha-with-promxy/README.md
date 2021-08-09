
# High Availability Prometheus with Promxy

## Summary

| Service      |              |                       |
|:-------------|--------------|-----------------------|
| am-01        | Alertmanager | http://localhost:8101 |
| am-02        | Alertmanager | http://localhost:8102 |
| am-03        | Alertmanager | http://localhost:8103 |
| prom-01      | Prometheus   | http://localhost:8201 |
| prom-02      | Prometheus   | http://localhost:8202 |
| promxy-01    | Promxy       | http://localhost:8801 |

## Description

Prometheus is a single process service not capable of running in a cluster by itself.

[Promxy](https://github.com/jacksontj/promxy) queries all Prometheus hosts in a server group and merges the responses. Gaps can still exist if not one of the duplicated Prometheus instances has samples for a period of time.

In this example, both Prometheus instances scrape themselves and the Alertmanagers. They share the same configuration files meaning they're _duplicated_.

The [configuration file for Promxy](promxy/config.yaml) is very simple, Promxy only needs to what server groups are.
