# Horizontal Pod Autoscaler

Horizontal Pod Autoscaler (HPA) scales the number of pod replicas based on observed resource usage.

## How it works
- HPA works with objects such as Deployments and ReplicaSets.
- It checks metrics from the Metrics Server.
- If CPU or memory usage increases, it can increase the replica count.
- If usage drops, it can reduce the replica count.

## Key idea
HPA focuses on scaling out or scaling in the number of pods.

## Important points
- It helps handle traffic spikes automatically.
- It improves resource efficiency.
- It uses metrics such as CPU utilization or custom metrics.

## Quick revision
- HPA changes replica count.
- It depends on Metrics Server for resource data.
- It is useful for workload scaling based on load.