# Kubernetes open standards

Kubernetes follows the same idea as OCI: it uses open standards and interfaces so that different implementations can plug into the platform without being tightly coupled to one vendor.

This makes Kubernetes more flexible, portable, and extensible.

## Why Kubernetes uses open standards
Kubernetes is designed to work with many components, such as:
- different container runtimes
- different networking plugins
- different storage providers
- different service mesh implementations

To support this, Kubernetes defines standard interfaces that external projects can implement.

## Common Kubernetes open standards

### 1) CRI - Container Runtime Interface
CRI is the interface between kubelet and the container runtime.

It standardizes how Kubernetes talks to runtimes such as:
- containerd
- CRI-O

It defines operations such as:
- starting and stopping containers
- pulling images
- monitoring container lifecycle

Example tools and technologies:
- containerd: a popular CRI-compatible container runtime
- CRI-O: a lightweight Kubernetes-native container runtime
- Docker is not the direct CRI implementation in modern Kubernetes setups, but containerd is commonly used behind the scenes

### 2) CNI - Container Network Interface
CNI is the standard interface for networking plugins in Kubernetes.

It is used to:
- assign IP addresses to Pods
- connect Pods to the network
- enable network policies and pod-to-pod communication

Examples include:
- Calico
- Flannel
- Cilium

Example tools and technologies:
- Calico: CNI plugin for network policy and routing
- Flannel: simple overlay networking
- Cilium: eBPF-based CNI plugin with advanced networking and security features

### 3) CSI - Container Storage Interface
CSI is the standard interface for storage plugins.

It enables Kubernetes to work with different storage backends for:
- persistent volumes
- dynamic provisioning
- volume attachment and mounting

Examples include:
- AWS EBS CSI driver
- Azure Disk CSI driver
- Ceph CSI driver

Example tools and technologies:
- AWS EBS CSI Driver: integrates Kubernetes with Amazon EBS
- Azure Disk CSI Driver: integrates Kubernetes with Azure managed disks
- Ceph CSI Driver: connects Kubernetes to Ceph storage

### 4) SMI - Service Mesh Interface
SMI is an interface for service mesh features in Kubernetes.

It helps standardize capabilities such as:
- traffic splitting
- traffic policy
- service identity and access control

It is mainly used in service-mesh-related integrations.

Example tools and technologies:
- Istio: a popular service mesh that supports service-mesh features
- Linkerd: a lightweight service mesh with traffic management capabilities
- Consul Connect: service mesh features for service-to-service communication

## KCNA exam takeaway
If you see a question about Kubernetes extensibility, remember these interfaces:
- CRI = container runtime integration
- CNI = networking integration
- CSI = storage integration
- SMI = service mesh integration

## Quick memory trick
- CRI → run containers
- CNI → connect containers in the network
- CSI → store container data
- SMI → manage service-mesh behavior
