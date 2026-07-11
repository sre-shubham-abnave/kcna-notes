We will discuss the DNS resolution done within the cluster


service dns has these component

Hostname: web-service ( service name)
Namespace: myapps 
Type: svc
Root: cluster.local

DNS name: web-service.myapps.svc.cluster.local


POD dns

Hostname: 10-244-2-5 (pod ip with dash separated)
Namespace: myapps 
Type: pod
Root: cluster.local

DNS name: 10-244-2-5.myapps.pod.cluster.local
