# Static Pods

Static Pods are managed directly by the `kubelet` on a node, not by the Kubernetes API server.

## How static Pods work
- A static Pod manifest is placed on a node in the directory `/etc/kubernetes/manifests`.
- The `kubelet` monitors that directory and automatically creates or updates the Pod based on the manifest file.
- Static Pods do not have a corresponding Pod object in the Kubernetes API server.

## Behavior
- If the manifest file is removed from `/etc/kubernetes/manifests`, the `kubelet` automatically deletes the static Pod.
- The `kube-scheduler` is not involved in static Pod creation.
- The Pod always runs on the node where its manifest file exists.

## Use cases
- Bootstrapping control plane components on a single-node cluster.
- Running node-level or bootstrap services before the cluster is fully functional.

## Notes
- Static Pods are useful when you need a Pod to exist on a node even if the API server is not available.
- Because static Pods are not managed through the API, features such as Deployments, ReplicaSets, and DaemonSets do not apply to them.
- Static Pods are typically used only for system or bootstrap workloads, not regular application workloads.

