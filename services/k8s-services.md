There are 3 types of services in kubernetes
NodePort
ClusterIP
LoadBalancer

Default type of service is ClusterIP
This is internall only service, that is created to enable communcation between applications within the cluster
If you want service to be accesible outside the cluster, you have to create service with type NodePort
this will make service avaible on predefined port on all the nodes in the cluster.

Load Balancer
This type of service is only sypported with specific cloud providers.This is like NodePOrt Service, but invokes a supported external load blancer


Service has their own IPs