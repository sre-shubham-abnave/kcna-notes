if you have only worker node and not master node, still you can schedule a pods on node. by using static pods

static pods can be created by placing a pod manifest file in the /etc/kubernetes/manifests directory on the node. The kubelet will automatically create and manage the pod based on the manifest file. Static pods are not managed by the Kubernetes API server, so they do not have a corresponding Pod object in the API.
if file is deleted form /etc/kubernetes/manifests directory, the kubelet will automatically delete the static pod from the node.


kube-scheduler is not involved in scheduling static pods, as they are created and managed directly by the kubelet on the node. This means that static pods will always be scheduled on the node where their manifest file is located, regardless of any scheduling constraints or policies that may be in place.
