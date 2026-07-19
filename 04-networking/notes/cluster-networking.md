# Cluster networking essentials

These are important Kubernetes networking and port concepts for KCNA revision.

## Control plane ports
- API server: port 6443
  - This is the main entry point for cluster access.
- kubelet: port 10250
  - Runs on both control plane and worker nodes.
- kube-scheduler: port 10259
  - Used by the scheduler process.
- kube-controller-manager: port 10257
  - Used by the controller manager.
- etcd client port: 2379
  - Used by clients to talk to etcd.
- etcd peer port: 2380
  - Used for etcd communication between members in a multi-master setup.

## NodePort service range
- Kubernetes uses ports 30000-32767 for NodePort services.

## KCNA exam takeaway
Know the common Kubernetes ports and their purpose, especially the API server, kubelet, scheduler, controller manager, and etcd.

Reference: https://kubernetes.io/docs/reference/networking/ports-and-protocols/