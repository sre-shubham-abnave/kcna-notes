# Service mesh

A service mesh is a dedicated layer for managing service-to-service communication in a microservices architecture.

## Why it is used
In modern applications, services talk to each other constantly. A service mesh helps manage this communication without changing application code.

## Main responsibilities
A service mesh typically handles:
- traffic management
- security
- observability
- service discovery
- health checks
- load balancing

## Common service mesh tools
- Istio
- Linkerd
- Consul Connect

## East-west traffic
In service mesh terminology, east-west traffic refers to traffic flowing between services inside the same data center or cluster.

This is different from north-south traffic, which is traffic entering or leaving the data center from clients or external systems.

### Example
- East-west traffic: service A calls service B inside the cluster
- North-south traffic: a user calls the application from outside the cluster

## Why this matters
Service meshes are especially useful for managing east-west traffic because internal service communication is often high-volume and needs features like retries, routing, mTLS, and visibility.

## KCNA exam takeaway
A service mesh helps manage internal service communication, especially east-west traffic, in a secure and observable way.