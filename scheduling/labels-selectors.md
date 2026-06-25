# Labels and selectors

- Labels are key/value pairs stored in `metadata.labels` of Kubernetes objects.
- Labels are used to categorize and select objects.
- You can add multiple labels to a Pod, Deployment, Service, or other resources.

## Select pods by label
```bash
kubectl get pods --selector environment=dev
# or use the shorthand
kubectl get pods -l environment=dev
```

## Labels and selectors relationship
- Kubernetes uses labels and selectors to connect objects such as ReplicaSets and Pods.
- A ReplicaSet can use `spec.selector.matchLabels` to select Pods with matching labels.
- The selected label set must match exactly for the Pod to be managed by the ReplicaSet.

Example:
- Pod metadata label: `environment: dev`
- ReplicaSet selector: `matchLabels:
    environment: dev`

## Annotations
- Annotations are separate from labels.
- They store arbitrary metadata such as build version, author name, or deployment information.
- Annotations are not used for scheduling or object selection.
