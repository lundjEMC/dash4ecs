# dash4ecs
Dashboard for ECS based on Prometheus/Grafana docker setup.

----------

The root contains a docker-compose configuration file that will start the following docker containers:

[prom/prometheus](https://hub.docker.com/r/prom/prometheus/ "the official docker image for prometheus") port:9090

[prom/node-exporter](https://hub.docker.com/r/prom/node-exporter/ "the official docker image for the prometheus node-exporter for machine metrics") port: 9100

[prom/pushgateway](https://hub.docker.com/r/prom/pushgateway "a metrics cache that allows ephemeral and batch jobs to expose their metrics to Prometheus") port:9091

[prom/collectd-exporter](https://hub.docker.com/r/prom/collectd-exporter "used to export metrics from existing collectd setups, and when metrics are not covered by the core Prometheus exporters (e.g. node-exporter)") port:9103

and

[grafana/grafana](https://hub.docker.com/r/grafana/grafana "the official Grafana docker image" ) port:3000

----------

Prometheus is configured to scrape data from itself, the node-exporter container running on the system where you install, the pushgateway and the collectd-exporter.  Currently the pushgateway and collectd-exporter do not have anything sending data their way, so they do not add any metrics yet.

Grafana needs to be set up initially (use admin/pass for system access).  Then you need to add Prometheus as a data source.  [Other data sources are supported by Grafana](http://docs.grafana.org/datasources/overview/) and can be configured (but are not installed/set up/configured by this code).

I've been playing with the collectd setup mentioned [here](https://github.com/jonasrosland/collectd-ecs), but don't feel comfortable enough to incorporate it here at this time.

Right now there is no code here that connects an ECS to this setup... that is the next step!

----------


To use:

1. clone or download the source to a linux system with [docker](https://docs.docker.com/engine/installation/) and [docker-compose](https://docs.docker.com/engine/installation/) installed.
2. ensure that you don't have anything using the default host ports OR change the default host ports in the docker-compose file and Prometheus configuration file as necessary.
3. from the directory where you download the source, run the following: 
`docker-compose -f prometheus_grafana_docker.yml up`
