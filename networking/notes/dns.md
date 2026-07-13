# DNS in Kubernetes

Kubernetes uses DNS for service discovery inside the cluster.

## CoreDNS
- CoreDNS is the standard DNS service used in Kubernetes clusters.
- It resolves names for Services and Pods.

## Service DNS format
A Service gets a DNS name in this format:
- service-name.namespace.svc.cluster.local

Example:
- web-service.myapps.svc.cluster.local

## Pod DNS format
A Pod gets a DNS name in this format:
- pod-ip-with-dashes.namespace.pod.cluster.local

Example:
- 10-244-2-5.myapps.pod.cluster.local

## KCNA exam takeaway
DNS helps Pods and Services discover each other by name, but DNS is not the feature that creates the pod network itself.
