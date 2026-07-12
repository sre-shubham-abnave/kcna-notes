# Prometheus Monitoring in Kubernetes

Prometheus is one of the most common tools used for monitoring Kubernetes clusters and applications.

## Why monitoring matters
Monitoring helps us answer questions like:
- Is the application healthy?
- Are pods restarting unexpectedly?
- Is CPU or memory usage too high?
- Are users seeing increased latency or errors?
- Is the cluster itself healthy?

## What can be monitored in Kubernetes

### 1. Application metrics
These show how your application is performing:
- request rate
- error rate
- response latency
- queue length
- business-specific metrics

### 2. Cluster metrics
These show the health of the Kubernetes environment:
- control plane components such as kube-apiserver, kube-scheduler, and controller-manager
- kubelet health
- node resource usage
- pod and deployment status

## Important Kubernetes monitoring components
- cAdvisor: exposes container-level metrics
- kube-state-metrics: provides object-level metrics such as deployments, pods, and replica sets
- node-exporter: collects host-level metrics like CPU, memory, disk, and network
- kubelet: exposes pod and container health information

## Prometheus basics
Prometheus is a pull-based monitoring system.
It scrapes HTTP endpoints exposed by targets and stores the data as time series.

### Key features
- collects metrics from targets
- stores data in a time-series database
- supports PromQL for querying and alerting
- works well for numeric time-series metrics

## Prometheus architecture
A basic Prometheus setup includes:
- Prometheus server: scrapes and stores metrics
- Exporters: expose application or system metrics in a Prometheus-friendly format
- Alertmanager: routes alerts to email, Slack, or other channels
- Grafana: visualizes dashboards

## Service discovery in Kubernetes
Prometheus can automatically discover pods and services in a cluster. This reduces manual configuration and makes dynamic environments easier to monitor.

## Kubernetes monitoring stack example
A common stack is:
- Prometheus for collection and querying
- Grafana for visualization
- Alertmanager for notifications
- kube-prometheus-stack for an easier deployment experience

## Helm-based installation example
You can deploy a common monitoring stack using Helm:

```bash
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack
```

## Important note
Prometheus is best for metrics. It is not a full replacement for logging or tracing systems. In real-world observability, you usually use metrics, logs, and traces together.

## Quick revision points
- Prometheus uses a pull model.
- Kubernetes monitoring needs both application and cluster metrics.
- kube-state-metrics and node-exporter are very important for cluster visibility.
- Service discovery makes monitoring easier in dynamic environments.
