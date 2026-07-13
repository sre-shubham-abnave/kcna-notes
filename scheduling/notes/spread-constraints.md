# Pod topology spread constraints

Pod topology spread constraints are used to control how Pods of the same workload are spread across different topology domains such as Nodes, Zones, or Regions.

## Primary purpose
The main purpose is to distribute Pods of a specific service evenly across the cluster so that:
- load is balanced better across Nodes
- the workload becomes more resilient to node failures
- resource usage is more uniform

In short, spread constraints help improve availability and balancing, not collocation.

## Why they are used
Use spread constraints when you want the scheduler to place Pods in a way that avoids concentrating too many replicas on the same Node or Zone.

This is especially useful for:
- stateless applications with multiple replicas
- high availability setups
- large clusters where uneven placement can cause hot spots

## Key fields
A topology spread constraint usually includes:

- `maxSkew`: how much imbalance is allowed between topology domains
- `topologyKey`: the label key used to define the domains (for example, `topology.kubernetes.io/zone` or `kubernetes.io/hostname`)
- `whenUnsatisfiable`: what to do if the constraint cannot be satisfied
  - `DoNotSchedule`: do not schedule the Pod if it would break the rule
  - `ScheduleAnyway`: try to satisfy the rule, but allow scheduling if not possible
- `labelSelector`: selects which Pods are considered for spreading

## Example
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 4
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      topologySpreadConstraints:
      - maxSkew: 1
        topologyKey: topology.kubernetes.io/zone
        whenUnsatisfiable: DoNotSchedule
        labelSelector:
          matchLabels:
            app: web-app
      containers:
      - name: web
        image: nginx
```

## Important distinction
Spread constraints are different from:
- `nodeAffinity`: tells the scheduler where Pods should prefer or require to run
- `anti-affinity`: prevents certain Pods from being placed together
- `taints/tolerations`: control which Pods can be placed on which Nodes

## KCNA quick notes
- Spread constraints help distribute replicas across Nodes/Zones.
- They improve load balancing and fault tolerance.
- They are configured in the Pod spec using `topologySpreadConstraints`.
- A common exam concept is: “spread Pods evenly across nodes/zones to avoid overloading one node.”
