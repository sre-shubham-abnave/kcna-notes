# Sidecars

A sidecar is an additional container that runs alongside the main application container in the same Pod.

## Why sidecars are used
Sidecars are often used to provide supporting features such as:
- logging
- monitoring
- file loading
- proxying traffic

## Important characteristics
- Sidecars share the same Pod network namespace
- They can share volumes with the main container
- They help extend the functionality of the main app without changing its code

## Relation to service mesh
In a service mesh, the sidecar proxy is often an Envoy container that manages service traffic for the main application container.

## KCNA exam takeaway
A sidecar is a helper container in the same Pod that supports the main application container.