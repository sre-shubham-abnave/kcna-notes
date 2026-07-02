# Resource requirements

Kubernetes lets containers declare resource `requests` and `limits` for CPU and memory.

## Resource requests
- `requests` specify the minimum resources a container needs.
- The scheduler uses requests to decide which node can host the Pod.

## Resource limits
- `limits` specify the maximum resources a container can use.
- CPU is throttled when a container exceeds its CPU limit.
- Memory is enforced by the kubelet and can cause the container to be terminated if it exceeds the memory limit.

## Example
```yaml
resources:
  requests:
    cpu: "100m"
    memory: "200Mi"
  limits:
    cpu: "200m"
    memory: "400Mi"
```

## Common combinations
1. No requests, no limits
   - The Pod has no guaranteed resources and can be scheduled only if the node has free capacity.
   - This results in `BestEffort` QoS.
2. No requests, limits
   - The scheduler treats the request as equal to the limit for scheduling purposes.
   - This results in `Burstable` QoS.
3. Requests and limits
   - The Pod has both guaranteed scheduling capacity and a hard cap on usage.
   - This is usually the recommended pattern.
4. Requests, no limits
   - The Pod is guaranteed the requested resources but may use more if available.
   - This also results in `Burstable` QoS.

## Quality of Service (QoS) classes
- `Guaranteed` — all containers in the Pod have requests and limits set, and they are equal.
- `Burstable` — containers have requests and limits set, but they are not all equal.
- `BestEffort` — no requests or limits are set.

## LimitRange
- `LimitRange` is a namespace-level object that can provide default requests and limits for Pods and containers.
- It can also set maximum and minimum values for resource usage in a namespace.

## Notes
- Always specify at least requests for production workloads so the scheduler can place Pods correctly.
- Limits are especially important for memory to avoid uncontrolled OOM behavior.
- Use `kubectl describe pod <pod-name>` to inspect the effective resource requests and limits.
