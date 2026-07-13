# Imperative vs Declarative

## Imperative approach
- Tell the system what to do step by step.
- You run commands that immediately create, update, or delete resources.
- It is harder to track changes over time because desired state is not stored declaratively.

Examples:
```bash
kubectl create -f nginx.yaml
kubectl delete -f nginx.yaml
kubectl edit deployment nginx
```

## Declarative approach
- Tell the system the desired state, and Kubernetes figures out how to reach it.
- Use manifest files and `kubectl apply` to manage resources declaratively.
- The desired state can be stored in version control and reconciled automatically.

Example:
```bash
kubectl apply -f nginx.yaml
```
