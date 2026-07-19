# kubectl apply

`kubectl apply` uses a declarative configuration file to create or update resources.

## Behavior
- Creates the object if it does not already exist.
- Updates the live object by comparing:
  - the local manifest file,
  - the last applied configuration, and
  - the live object state.

## Last applied configuration
- Kubernetes stores the last applied configuration in the object annotation `kubectl.kubernetes.io/last-applied-configuration`.
- This annotation is used to compute the diff and patch when running `kubectl apply` again.

## Example
```bash
kubectl apply -f nginx.yaml
```

## Notes
- `kubectl apply` is the recommended declarative workflow for managing resources.
- Use `kubectl diff -f nginx.yaml` to preview changes before applying them.
