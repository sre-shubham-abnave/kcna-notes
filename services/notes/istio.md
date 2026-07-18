# Istio

Istio is a popular open-source service mesh.

## Key idea
Istio adds traffic management, security, and observability for microservices without requiring application code changes.

## Architecture
Istio uses:
- Envoy proxies as sidecars
- a control plane to manage configuration

## Control plane components
Istio typically includes components such as:
- Pilot: traffic management and routing configuration
- Citadel: security and identity features
- Galley: configuration validation and distribution

## Sidecar model
Each pod in an Istio-enabled application can have an Envoy sidecar proxy. The sidecar handles communication in and out of the application container.

## KCNA exam takeaway
Istio is a service mesh platform that uses Envoy proxies to manage service-to-service traffic.