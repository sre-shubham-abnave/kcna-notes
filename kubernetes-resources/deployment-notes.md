# Deployment rollout notes

## Check rollout status
```bash
kubectl rollout status deployment.apps/myapp-deployment
```

## View rollout history
```bash
kubectl rollout history deployment.apps/myapp-deployment
```

## Annotate a deployment
```bash
kubectl annotate deployment myapp-deployment kubernetes.io/change-cause="Using annotate command to add change cause"
```

## Update deployment image
```bash
kubectl set image deployment myapp-deployment nginx=1.29.8
```

## Rollback deployment
```bash
kubectl rollout undo deployment myapp-deployment
```

## Deployment strategy notes
When Kubernetes updates a Deployment by changing the container image or Pod template, it uses a deployment strategy to replace old Pods with new ones.

### 1. RollingUpdate (default)
- Replaces Pods gradually.
- Keeps some old and some new Pods running during the rollout.
- Provides zero downtime.
- Best for web apps and services that can handle a mixed version state temporarily.

### 2. Recreate
- Terminates all old Pods first.
- Starts new Pods after the old ones are gone.
- Causes downtime.
- Best when running old and new versions together could cause issues, such as data corruption.

### YAML example: RollingUpdate
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-rolling
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: web
        image: nginx:1.25.1
```

### YAML example: Recreate
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-recreate
spec:
  replicas: 3
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: web
        image: nginx:1.25.1
```

## Notes
- `kubectl rollout status` shows the current rollout progress for a deployment.
- `kubectl rollout history` shows revision history for a deployment.
- `kubectl annotate` can add metadata such as change causes.
- `kubectl rollout undo` rolls back to the previous revision.
