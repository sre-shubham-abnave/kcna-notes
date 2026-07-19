Kubernetes exposes a REST API via the `kube-apiserver`. You can call it directly or via `kubectl`.

## Calling the API directly with curl
If you call the API server directly you must present valid credentials and trust the server's certificate.

Example (certificate authentication):
```bash
curl --cacert kind-ca.crt --cert kcna-client.crt --key kcna-client.key \
  https://127.0.0.1:61503/api/v1/pods
```

If you do not want to manage TLS credentials yourself, use `kubectl proxy` which reads your kubeconfig and runs a local HTTP proxy:

```bash
kubectl proxy
# then use the proxy without manually passing certs:
curl http://localhost:8001/api/v1/pods
```

## kubeconfig and credentials
- Your kubeconfig contains cluster information (server, CA), user credentials (client cert/key or token), and contexts.
- `kubectl` automatically uses the credentials in kubeconfig for API requests.

## API groups and resources
- The API is organized into groups: the core group (no prefix, e.g., `/api/v1`) and named groups (e.g., `/apis/apps/v1`, `/apis/networking.k8s.io/v1`).
- Each resource supports standard verbs such as `get`, `list`, `create`, `update`, `delete`.

## Notes
- When calling the API directly, ensure you have appropriate RBAC permissions; otherwise requests will be denied with `403`.
- Use `kubectl api-resources` and `kubectl get --raw` to explore the API surface.
