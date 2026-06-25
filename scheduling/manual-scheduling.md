# Manual scheduling

Manual scheduling is when a Pod is assigned to a specific node explicitly.
This is usually not the recommended production approach, but it is useful for learning or specific control cases.

## Ways to schedule manually
- `spec.nodeName`: force a Pod onto a specific node by name.
- `spec.nodeSelector`: match node labels to choose a node.

## Example: nodeName
```yaml
spec:
  nodeName: node-1
```

## Example: nodeSelector
```yaml
spec:
  nodeSelector:
    disktype: ssd
```

## Notes
- `spec.nodeName` bypasses normal scheduling and places the Pod directly on the named node.
- `nodeSelector` uses node labels and is more flexible than hard-coding a node name.
- Check node labels with:
```bash
kubectl get nodes --show-labels
```
