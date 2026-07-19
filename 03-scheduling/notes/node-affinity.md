# Node affinity

Node affinity lets you specify rules about which Nodes a Pod is eligible to be scheduled on, using Node labels.
It provides a richer, declarative way to express where Pods should (or should preferably) run.

There are two main nodeAffinity types (as shown in your screenshot):

- `requiredDuringSchedulingIgnoredDuringExecution` (Type 1 — Required during scheduling, ignored during execution)
	- The rule is a hard requirement at scheduling time: Pods that do not match will not be scheduled onto the Node.
	- The scheduler enforces this only when placing the Pod. If Node labels change later, the running Pod is not evicted.

- `preferredDuringSchedulingIgnoredDuringExecution` (Type 2 — Preferred during scheduling, ignored during execution)
	- This is a soft preference: the scheduler will try to place the Pod on Nodes that match the preference, but it can place the Pod elsewhere if needed.
	- Like the required type, the preference is ignored for eviction during execution.

Both types use the same `matchExpressions` vocabulary for rules.

## Operators available in node affinity
The following operators are valid in `matchExpressions` for node affinity and are useful to know for KCNA:

- `In` — the node label value must be one of the listed values.
- `NotIn` — the node label value must not be any of the listed values.
- `Exists` — the key must exist on the node (value is ignored).
- `DoesNotExist` — the key must not exist on the node.
- `Gt` — the node label value (interpreted as integer) must be greater than the specified value.
- `Lt` — the node label value (interpreted as integer) must be less than the specified value.

## Examples

1) Required node affinity (hard requirement):

```yaml
affinity:
	nodeAffinity:
		requiredDuringSchedulingIgnoredDuringExecution:
			nodeSelectorTerms:
			- matchExpressions:
				- key: disktype
					operator: In
					values:
					- ssd
```

2) Preferred node affinity (soft preference):

```yaml
affinity:
	nodeAffinity:
		preferredDuringSchedulingIgnoredDuringExecution:
		- weight: 100
			preference:
				matchExpressions:
				- key: cpu-type
					operator: In
					values:
					- arm
```

3) Examples of `matchExpressions` using each operator:

- `In`:
```yaml
matchExpressions:
	- key: env
		operator: In
		values: [dev, staging]
```

- `NotIn`:
```yaml
matchExpressions:
	- key: env
		operator: NotIn
		values: [prod]
```

- `Exists`:
```yaml
matchExpressions:
	- key: gpu
		operator: Exists
```

- `DoesNotExist`:
```yaml
matchExpressions:
	- key: maintenance
		operator: DoesNotExist
```

- `Gt` / `Lt` (numeric comparison — node label values must be parseable as integers):
```yaml
matchExpressions:
	- key: nvidia.com/gpu-count
		operator: Gt
		values: [0]
	- key: cores
		operator: Lt
		values: [8]
```

## Quick notes for KCNA
- `requiredDuringSchedulingIgnoredDuringExecution` = hard requirement at scheduling time.
- `preferredDuringSchedulingIgnoredDuringExecution` = soft preference at scheduling time.
- Both are ignored for eviction during execution (hence the `IgnoredDuringExecution` suffix).
- Use nodeAffinity (or nodeSelector) when you want to steer or guarantee Pod placement; combine with taints/tolerations when you need to repel or allow Pods on nodes.

If you want, I can also add a full Pod manifest example that demonstrates both a `required` and `preferred` rule together.

