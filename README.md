# DIY alert analysis

Alert analysis tool gathers alerts from webhook and Alertmanager API, stores it in ClickHouse database and 
provides dashboards for analyzing the data.
Please refer to [Cloudflare Blog](https://blog.cloudflare.com/alerts-observability) for insights and experiences 
and [PromCon 2023 in Berlin](https://promcon.io/2023-berlin/talks/alert-analytics/) for the talk presentation.

This demo uses `vector.dev` to collect data from different sources and write the data in the datastore.
we use one `http_server` vector instance - to receive Alertmanager webhook notifications,
two `http_client` sources to query Alertmanager's alerts and silence API endpoints and
two `sinks` for writing all the state logs in ClickHouse into `alerts` and `silences` tables.

The docker-compose will bring up several containers:

* `Cadvisor` is used to generate system metrics for monitoring.
* `Prometheus` is used to monitor and generate alerts.
* `Alertmanager` is to route alerts and provide the alert events via webhook and API.
* `alertmanager_silence` is to create an Alertmanager silence.
* `blackbox_exporter` is for monitoring the sites and generating alerts.
* `ClickHouse` is used to write the Alertmanager alert events into the datastore for alert analysis.
* `Vector.dev` - to collect data from Alertmanager webhook, alerts and silences API, transform the data and write into ClickHouse.
* `Grafana` is used to visualize the logs.

## Pre-requisite:
`docker`

## Getting started:

Bring up the containers using docker compose
```docker compose up```

Please wait for about 5 minutes for the alerts to be triggered and
visit http://localhost:3000/ to explore the `Alerts and silences overview` dashboard and play around.

![alerts and silences overview](images/alerts-silences-overview.png "alerts and silences overview")
