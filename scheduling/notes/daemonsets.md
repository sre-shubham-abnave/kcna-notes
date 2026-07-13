# DaemonSet

A `DaemonSet` ensures that a copy of a Pod runs on every node in the cluster, or on a selected subset of nodes.

## Key behavior
- When a new node joins the cluster, the DaemonSet automatically creates a Pod on that node.
- When a node is removed, the DaemonSet removes the Pod from that node.
- A DaemonSet is useful for node-level agents and system services.

## Use cases
- Log collectors such as `promtail`
- Monitoring agents such as `node-exporter`
- Networking agents such as `kube-proxy`
- Host-level security or audit daemons

## DaemonSet vs ReplicaSet
- A `ReplicaSet` manages a specified number of Pod replicas and does not guarantee one Pod per node.
- A `DaemonSet` targets node coverage, ensuring one Pod per matching node.

## Notes
- Use node selectors or affinities inside a DaemonSet manifest if you want it on only a subset of nodes.
- DaemonSets are commonly used for cluster-level infrastructure components that must run on every node.
