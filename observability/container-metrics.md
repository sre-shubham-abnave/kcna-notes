# Container Metrics

Container metrics help us understand how much resources each container is using and how healthy it is.

## Docker engine metrics
These metrics describe the Docker daemon itself, not individual containers.

Examples:
- CPU used by Docker
- number of failed image builds
- time taken to process container actions

## cAdvisor metrics
cAdvisor collects metrics directly from containers.

Examples:
- CPU usage per container
- memory usage per container
- number of running processes inside a container
- container uptime
- per-container resource consumption

## Why container metrics matter
They help identify:
- resource-heavy containers
- memory leaks
- CPU bottlenecks
- unhealthy or restarting containers

## Quick revision
- Docker engine metrics are host-level daemon metrics.
- cAdvisor provides container-level metrics.
- These metrics are important for performance monitoring and debugging.