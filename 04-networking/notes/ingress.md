# Ingress

Ingress is a Kubernetes resource used to expose HTTP and HTTPS routes from outside the cluster to Services inside the cluster.

## Key idea
- Ingress works at Layer 7 of the OSI model.
- It is commonly used for path-based and host-based routing.
- It is often managed by an Ingress controller such as:
  - NGINX Ingress Controller
  - Traefik
  - HAProxy

## Difference from Service types
- Service type LoadBalancer exposes traffic at the Service level.
- Ingress provides routing rules to one or more Services.

## KCNA exam takeaway
Ingress is used for smart traffic routing to applications, especially for web traffic using hostnames and paths.