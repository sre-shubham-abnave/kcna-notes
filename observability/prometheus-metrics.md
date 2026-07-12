# Prometheus Metrics

Prometheus metrics are collected as time-series data.
Each metric consists of:
- metric name
- labels
- value
- timestamp

## Example
```text
node_cpu_seconds_total{cpu="0",mode="idle"} 23456.55
```

## Time series
A time series is a stream of values over time for the same metric and label set.

Example:
- `node_filesystem_files{device="sda2",instance="server1"}`
- `node_filesystem_files{device="sda3",instance="server2"}`

Each unique combination of metric name and labels forms a separate time series.

## Metric types
Every metric has metadata such as:
- help: description of the metric
- type: type of the metric

### Counter
- only increases
- used for counting events
- examples: total requests, total errors, total jobs executed

### Gauge
- can go up and down
- used for current values
- examples: CPU usage, memory usage

### Histogram
- records observations in buckets
- useful for measuring sizes or durations
- example: request latency buckets

### Summary
- also measures size or duration
- provides quantiles and counts

## Labels
Labels are key-value pairs attached to a metric.
They help distinguish different instances or dimensions.

Examples:
- instance
- job
- environment
- region

## Quick revision
- Prometheus stores data as time series.
- Metrics can be counters, gauges, histograms, or summaries.
- Labels add context to metrics and enable better filtering.