# Volumes in Kubernetes

## Why do we need volumes?
Pods are temporary. If a pod is deleted, the data stored inside its container filesystem is usually lost. A volume gives a pod a place to store data that should survive pod restarts or pod deletion.

## Key concept
- A container filesystem is ephemeral.
- A volume is mounted into a container at a specific path.
- Data written to the volume remains available as long as the volume exists.

## Common volume types

### 1. EmptyDir
- Temporary storage shared by containers in the same pod.
- Useful for cache, scratch data, or sharing data between containers.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: shared-data
spec:
  containers:
  - name: container1
    image: busybox
    command: ["sh", "-c", "echo hello > /data/index.txt && sleep 3600"]
    volumeMounts:
    - name: shared-volume
      mountPath: /data
  - name: container2
    image: busybox
    command: ["sh", "-c", "sleep 3600"]
    volumeMounts:
    - name: shared-volume
      mountPath: /data
  volumes:
  - name: shared-volume
    emptyDir: {}
```

### 2. HostPath
- Mounts a directory from the node's filesystem.
- Useful for learning and testing, but not ideal for production.

```yaml
volumes:
- name: data-volume
  hostPath:
    path: /data
    type: Directory
```

### 3. PersistentVolumeClaim
- Used to attach persistent storage provided by a PersistentVolume.
- This is the standard Kubernetes way for applications to request storage.

### 4. ConfigMap and Secret as volumes
- Mount configuration files and sensitive data into containers.

## Exam points
- `volumes` is defined at the pod level.
- `volumeMounts` is defined inside each container.
- Volumes help persist data beyond the container lifecycle.


