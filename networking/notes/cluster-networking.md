master node should accept connection on port 6443

kubelet on master and worker node listen on 10250 port
kube scheuduler required port 10259 to be open
kube controller manager rquires 10257
etcd server listens on 2379
if we have multiple master, than etcd clients commumicate with each other on port 2380
worker nodes expose services on this port range: 30000-32767

Documentation : https://kubernetes.io/docs/reference/networking/ports-and-protocols/