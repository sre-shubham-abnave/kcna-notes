# Persistent Volume and Persistent Volume Claim

## Overview
Kubernetes separates storage provisioning from storage usage:
- PersistentVolume (PV): storage resource created by an administrator.
- PersistentVolumeClaim (PVC): storage request made by a user or application.

## Relationship between PV and PVC
- An administrator creates a PV.
- A user creates a PVC to request storage.
- A PVC binds to a matching PV.
- The relationship is usually one-to-one.
- Once a PV is bound to a PVC, it cannot be used by another claim.

## Access Modes
A PV can support different access modes:
- ReadWriteOnce: one node can read and write.
- ReadOnlyMany: multiple nodes can read.
- ReadWriteMany: multiple nodes can read and write.

## Reclaim Policy
When a PVC is deleted, Kubernetes uses a reclaim policy to decide what happens to the PV:
- Retain: keep the data and PV for manual cleanup.
- Delete: delete the underlying storage resource.

## Important exam points
- If no matching PV is available, the PVC stays in `Pending` state.
- PVCs are used by pods through `persistentVolumeClaim` in the pod spec.
- PVs are cluster-level storage resources.

## Example
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-vol1
spec:
  storageClassName: ""
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 1Gi
  hostPath:
    path: /tmp/data
```
