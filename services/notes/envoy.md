# Envoy

Envoy is an open-source high-performance proxy.

## Role in Kubernetes
Envoy is commonly used as a sidecar proxy in service meshes like Istio and Linkerd.

## What it does
It handles:
- inbound traffic to a service
- outbound traffic from a service
- traffic routing, retries, and observability

## Why it is important
Because it runs as a sidecar, it can manage communication between services without changing the main application code.

## KCNA exam takeaway
Envoy is a proxy used to control and observe service traffic in service mesh architectures.