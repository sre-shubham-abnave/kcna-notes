# Prometheus Architecture

Prometheus works in a simple flow:
1. It scrapes metrics from targets.
2. It stores the collected data in a time-series database.
3. It serves queries through PromQL.

## Main components
- Prometheus server: scrapes data, stores it, and answers queries.
- Exporters: expose metrics from applications or systems in a format Prometheus can read.
- Alertmanager: handles alerts and sends notifications.
- Grafana: visualizes metrics and dashboards.

## Pull-based model
Prometheus follows a pull-based model.
It sends HTTP requests to configured targets and collects their metrics.

## Exporters
Exporters are small components that convert internal application or system data into Prometheus-compatible metrics.

## Pushgateway
For short-lived jobs, the normal pull model may not work well. In such cases, Prometheus can use Pushgateway so the job can push metrics before it exits.

## Service discovery
In dynamic environments, manually adding targets is not practical. Prometheus can discover targets automatically using Kubernetes service discovery and other integrations.

## Quick revision
- Prometheus collects metrics by scraping.
- Exporters expose data in Prometheus format.
- Pushgateway helps with short-lived jobs.
- Service discovery makes target management easier.