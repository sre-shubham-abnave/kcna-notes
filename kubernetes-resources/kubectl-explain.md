# kubectl explain

Use `kubectl explain` to inspect API resources and fields.

## List all resources
```bash
kubectl api-resources
```

## Explain a specific resource
```bash
kubectl explain pods
```

## Explain a nested field
```bash
kubectl explain pods.spec
```

## Notes
- `kubectl explain <resource>` shows the API schema for a resource.
- `kubectl explain <resource>.<field>` shows field definitions and nested fields.
- Add `--recursive` to display all nested fields, for example:
```bash
kubectl explain pods.spec --recursive
```

