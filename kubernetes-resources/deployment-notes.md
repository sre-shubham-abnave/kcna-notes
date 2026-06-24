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

## Notes
- `kubectl rollout status` shows the current rollout progress for a deployment.
- `kubectl rollout history` shows revision history for a deployment.
- `kubectl annotate` can add metadata such as change causes.
- `kubectl rollout undo` rolls back to the previous revision.
