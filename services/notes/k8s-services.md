# Kubernetes Services

A Kubernetes Service provides a stable endpoint to access a group of Pods.

## Why Services are needed
Pods are temporary and can be replaced, restarted, or scaled. Because of that, Pod IP addresses are not stable.

A Service solves this by giving your application a stable name and IP that stays in place while the backend Pods change.

## Key purpose
Services help with:
- stable access to workloads
- service discovery inside the cluster
- load balancing across Pods

## Common Service types
- ClusterIP
  - default type
  - exposes the Service only inside the cluster
- NodePort
  - exposes the Service on a port of each node
  - used for external access
- LoadBalancer
  - creates an external load balancer through the cloud provider
  - used for internet-facing access

## KCNA exam takeaway
A Service gives a stable abstraction over dynamic Pods, making communication reliable and easier to manage.