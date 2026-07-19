# Container Network Interface (CNI)

CNI is the standard interface used by Kubernetes to configure networking for Pods.

## How it works
When a container is created or deleted, the container runtime calls a CNI plugin to:
- create or remove the network namespace
- attach the container to the correct network
- assign an IP address
- set up routing and connectivity

## Important CNI details
- CNI plugins are installed in: /opt/cni/bin
- The plugin to use is configured in: /etc/cni/net.d
- The configuration is usually stored in JSON format

## Common CNI plugins
- Calico
- Flannel
- Cilium

## KCNA exam takeaway
Kubernetes does not implement pod networking by itself. It relies on third-party CNI plugins to provide the pod network and IP connectivity.