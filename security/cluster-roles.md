 There are two types of resources in k8s, Namespaces and cluster Scoped
 Namespaced exmaple - pods, replicasets, roles, rolebinding, pvc
 Cluster scoped - nodes, PV, clusterrole, clusterrolebindings

 If you want to access cluster scoped resources, you cannot use role and rolebinding, so for that we have to use clusterrole and clusterrolebinding

 Cluster role are same as roles, just difference is they are used for cluster scoped resources

 Also , Cluster roles can be used for namespaced scoped resources and cluster scoped resources both.