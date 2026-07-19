# Prometheus Basics

Prometheus is an open-source monitoring and alerting system.
It is widely used for collecting and analyzing metrics from applications and infrastructure.

## Key features
- collects metrics by scraping HTTP endpoints
- stores data in a time-series database
- supports alerts and notifications
- supports querying using PromQL
- works well with dashboards and visualization tools

## What Prometheus is good at
Prometheus is best for monitoring numeric time-series data such as:
- CPU usage
- memory usage
- request count
- response time
- error rate

## What Prometheus is not ideal for
Prometheus is not the best tool for:
- logs
- full event streams
- distributed tracing

These are usually handled by other tools such as Loki, Elasticsearch, or Jaeger.

## Quick summary
Prometheus is mainly used for metrics-based monitoring, alerting, and visualization.