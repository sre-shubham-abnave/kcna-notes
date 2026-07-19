# Pod networking

Kubernetes defines a specific pod networking model.

## Core rules
- Every Pod should have its own unique IP address.
- Pods on the same node should be able to communicate with each other.
- Pods on different nodes should also be able to communicate with each other without NAT.

## Important concept
This creates a flat network model, where Pods behave like they are on the same large network even if they are running on different Nodes.

### What "flat network" means
A flat network means that Pods can reach each other directly by IP address without needing special routing tricks or NAT between Nodes. In other words, Pod A on Node 1 can talk to Pod B on Node 2 as if both were on the same local network.

This is a key Kubernetes networking principle because it makes communication between Pods simple and consistent.

## How this is implemented
Kubernetes does not provide the pod network itself. It uses third-party CNI plugins to implement the network.

## KCNA practice question
Question:
What feature does Kubernetes use to implement the pod network to create a large, flat open network that pods can use to communicate on?

Correct answer:
Third-party Container Network Interface (CNI) plugins.

### Explanation
CNI plugins are responsible for:
- assigning IP addresses to Pods
- attaching Pods to the cluster network
- enabling communication between Pods across Nodes

Popular examples include:
- Calico
- Flannel
- Cilium

## KCNA exam takeaway
Pod networking is implemented by CNI plugins, not by DNS, load balancers, or static IP addresses alone.