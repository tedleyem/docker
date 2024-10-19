# influxdb-v1-grafana system monitoring app

Multi-container System monitoring with Grafana and Influxdb

* [InfluxDB](https://github.com/influxdata/influxdb) - time series database
* [Chronograf](https://github.com/influxdata/chronograf) - admin UI for InfluxDB
* [Grafana](https://github.com/grafana/grafana) - visualization UI for InfluxDB

## Services

The services in Grafana run on the following ports:

| Host Port | Service |
| - | - |
| 3000 | [Grafana](http://127.0.0.1:3000) |
| 8086 | [InfluxDB](http://127.0.0.1:8086) |
| 8888 | [Chronograf](http://127.0.0.1:8888) |


## Quick Start

To start Grafana:

1. Run the following command:
```
docker-compose up -d
```


2. Connect to Influxdb and create a bucket
```
http://localhost:8086/onboarding
```

3. Copy API token shown after your db is setup

4. login to Grafana
```
http://localhost:3000/
```

5. Use the data from influxdb to connect as a Datasource


6. Import Influxdb interal dashboard from [grafana dashboards](https://grafana.com/grafana/dashboards/421-influxdb-internals/)

InfluxDB Internals:  421 [link](https://grafana.com/orgs/failfish)
Telegraf system dashboard: 914 [link](https://grafana.net/dashboards/914)
InfluxDB Docker [link](https://grafana.net/dashboards/914)
InfluxDB 2.x Telegraf Docker Dashboard: 18389 [link](https://grafana.com/grafana/dashboards/18389-influxdb-2-x-telegraf-docker-dashboard/)
Docker Dashboard: 91838 [link](https://grafana.com/grafana/dashboards/10585-docker-dashboard/)

## Users

Grafana creates two admin users - one for InfluxDB and one for Grafana. By default, the username and password of both accounts is `admin`. To override the default credentials, set the following environment variables before starting Grafana:

* `INFLUXDB_USERNAME`
* `INFLUXDB_PASSWORD`
* `GRAFANA_USERNAME`
* `GRAFANA_PASSWORD`

## Database

Grafana creates a default InfluxDB database called `db0`.
To change this you can
change the docker-compose.yml parameter INFLUXDB_DB=db0

## Data Sources

Grafana will create a Grafana data source called `InfluxDB` that's connected to the default IndfluxDB database (e.g. `db0`).

To provision additional data sources: see the Grafana [documentation](http://docs.grafana.org/administration/provisioning/#datasources) and add a config file to `./grafana-provisioning/datasources/` before starting Grafana.

## Dashboards

To add more dashboards: checkout the Grafana [documentation](http://docs.grafana.org/administration/provisioning/#dashboards) and add a config file to `./grafana-provisioning/dashboards/` before starting Grafana.
