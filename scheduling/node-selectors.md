# NodeSelector

`nodeSelector` is the simplest way to constrain a Pod to run on Nodes that have specific labels.

## Label a node
Use `kubectl label nodes` to add labels to nodes:

```bash
kubectl label nodes <node-name> key=value
# example:
kubectl label nodes kcna-worker size=Large
```

## Use `nodeSelector` in a Pod spec
`nodeSelector` requires an exact match of node labels. If the node has all the key/value pairs specified, the Pod can be scheduled there.

```yaml
spec:
	nodeSelector:
		size: Large
```

## Limitations
- `nodeSelector` only supports exact matches (key=value). It does not support logical operators, lists, or numeric comparisons.
- For more flexible rules (preferences, multiple operators, or numeric comparisons), use `nodeAffinity`.

## When to use
- Use `nodeSelector` for simple, exact label matches.
- Use `nodeAffinity` for advanced scheduling rules (required/preferred, operators like `In`, `Exists`, `Gt`, etc.).

## Notes
- `nodeSelector` is equivalent to a single `nodeAffinity` rule with `requiredDuringSchedulingIgnoredDuringExecution` and a simple `matchExpressions` set to `In` with one value.
- Always ensure your nodes are labeled before creating Pods that depend on those labels.