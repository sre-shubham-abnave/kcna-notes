# Taints and tolerations

Taints and tolerations control which Pods can be scheduled onto which Nodes.
- A taint is applied to a Node.
- A toleration is applied to a Pod.

If a Pod tolerates a Node's taint, it is eligible to be scheduled onto that Node.
If it does not tolerate the taint, the Pod is not scheduled there.

## Taint analogy
- A taint is like a shield on a Node.
- A toleration is like a key the Pod carries.
- Only Pods with the correct toleration can pass through the taint filter.

## Apply a taint to a node
```bash
kubectl taint nodes node-name key=value:NoSchedule
```

## Taint effects
- `NoSchedule`
  - Pods that do not tolerate this taint will not be scheduled on the node.
  - Existing Pods are not evicted.
- `PreferNoSchedule`
  - The scheduler will try to avoid placing Pods that do not tolerate the taint on the node.
  - It is a soft preference, not a hard rule.
- `NoExecute`
  - Pods that do not tolerate this taint will be evicted if they are already running on the node.
  - New Pods that do not tolerate the taint will not be scheduled on the node.

## Example toleration
```yaml
tolerations:
- key: "key"
  operator: "Equal"
  value: "value"
  effect: "NoSchedule"
```

## Notes
- Taints do not schedule Pods by themselves; they only repel Pods that do not tolerate them.
- A Pod can tolerate multiple taints.
- `NoExecute` is the only effect that can evict existing Pods from a Node.
