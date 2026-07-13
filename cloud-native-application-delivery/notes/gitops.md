Gitops working group comes undert K8s App delivery SIG


Open gitops project gives us Four core principles

1. Declarative
intire system has to be diescribed declaratively.

2.Version and Immutable

3. Pull automatically
approved changes should automaticallly applied to the system

4. Continuously reconsile



Push vs Pull based deployment

For push based system, you may need to provide your k8s creds to your pipeline, which can be harmful

Pull based - 
All changes are made within cluster so we dont have to give creds to the other systems.



CI / CD with gitops

Applicaiton code repo
Kubernets manifest repository

To implement gitops, we use operator like ArgoCD which runs inside k8s cluster
It will continuously monitor kuberntes manifest repo for changes and reconsiles the desired state with the actual state 