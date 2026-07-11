# Storage Class

## What is a StorageClass?
A StorageClass is a Kubernetes object that defines how storage should be dynamically provisioned.

## Static vs Dynamic provisioning
- Static provisioning: an administrator manually creates the storage and the PV.
- Dynamic provisioning: Kubernetes creates the PV automatically when a PVC requests storage.

## Why use StorageClass?
With a StorageClass, you do not need to manually create a PV every time an application asks for storage. The StorageClass tells Kubernetes which storage provisioner to use.

## How it works
1. Create a StorageClass with a provisioner.
2. Create a PVC and set `storageClassName`.
3. Kubernetes creates a matching PV automatically.
4. The pod mounts the PVC and uses the storage.

## Example
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: google-storage
provisioner: kubernetes.io/gce-pd
```

## Exam points
- StorageClass enables dynamic provisioning.
- PVCs reference a StorageClass using `storageClassName`.
- Parameters inside the StorageClass can define storage tier, replication, or performance level.
