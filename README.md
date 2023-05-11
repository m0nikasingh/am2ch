# am2ch

am2ch runs vector.dev instance as a HTTP server, receives HTTP webhook notifications from AlertManager and inserts them into ClickHouse

This demo collects alert details from Alertmanager, transforms the data using vector.dev and writes it in the datastore for analytics.

The docker-compose would spawn up 7 containers:

* cadvisor - for generating system metrics for monitoring
* prometheus - to monitor and generate alert
* alertmanager - to route alerts and provide the alert events via webhook and API
* blackbox_exporter - for monitoring the sites and generate alerts
* clickhouse - to write the alertmanager alert events into the datastore for alert anaytics
* Vector.dev - to collect data from alertmanager webhook, alerts api and silences api, transform the data and write into ClickHouse.
* Grafana - to visualize the logs

Pre-requisite:

docker
Getting started:

Bring up the containers using docker compose

```docker compose up```
And visit http://localhost:3000/ and open the Demo dashboard, play around.
This is a very basic dashboard.
