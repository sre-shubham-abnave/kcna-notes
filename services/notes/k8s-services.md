# Kubernetes Services Notes

## What is a Service?
In Kubernetes, a Service provides a stable way to access a group of Pods.
It solves the problem of dynamic Pod IPs by giving applications a fixed endpoint to use.

## Why Service Discovery is needed
In a traditional server setup, an app might use a fixed IP address such as `192.168.1.50`.
In Kubernetes, Pods are temporary and can be created, restarted, or replaced at any time.
Each new Pod may receive a different IP address.

Because of this:
- Pods are ephemeral.
- IP addresses change frequently.
- unhealthy Pods should be removed from traffic automatically.

If frontend apps tried to talk to individual Pod IPs directly, the application would break often.

## How Service Discovery works
A Kubernetes Service acts like a dynamic phone book and traffic router.
- The Service gets a stable name such as `backend-service`.
- Clients connect to the Service name instead of individual Pod IPs.
- Kubernetes uses readiness probes and health checks to send traffic only to healthy Pods.

This makes communication reliable even when Pods are replaced or scaled.

## Types of Services
1. ClusterIP
   - Default type.
   - Internal-only service.
   - Used for communication inside the cluster.

2. NodePort
   - Exposes the Service on a static port on each node.
   - Used to make the Service accessible from outside the cluster.

3. LoadBalancer
   - Works with cloud providers to create an external load balancer.
   - Used when you want external traffic routed to the Service.

## Important point
A Service has its own stable virtual IP and DNS name, while the underlying Pods may change frequently.

## Quick revision
- Services provide stable access to dynamic Pods.
- Service Discovery helps clients find healthy backends automatically.
- Kubernetes uses readiness and routing logic to avoid sending traffic to unhealthy Pods.