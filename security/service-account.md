ServiceAccounts — quick reference

- **Users** are for humans. **ServiceAccounts** are for processes running in Pods.
- A default ServiceAccount is created in each namespace; Pods use a ServiceAccount via `spec.serviceAccountName`.

## Inspect ServiceAccounts
```bash
kubectl get serviceaccounts -n <namespace>
kubectl describe sa testing-sa -n <namespace>
```

## Automatic in-cluster token mounting
- By default, the kubelet mounts a projected ServiceAccount token into the Pod at:
	`/var/run/secrets/kubernetes.io/serviceaccount`.
- The mounted files include `token`, `namespace`, and `ca.crt` (used to validate the API server).
- The token is rotated by the kubelet and is tied to the Pod's lifetime.

## Disable automatic mount
- `automountServiceAccountToken: false` (pod-level or serviceAccount-level) prevents the kubelet from automatically mounting the token into the Pod.
- Disabling the auto-mount reduces the attack surface when the workload does not need Kubernetes API access.

## If the token is not mounted — can the Pod still run?
- Yes. The token is not required for the container runtime or scheduling; it is only needed if the application inside the Pod needs to call the Kubernetes API.

## Provide credentials to the Pod intentionally
Two common approaches when a Pod must call the API but you want explicit control over credentials:

Option A — Create a token and mount it as a Secret (useful for external tools)
1. Create a ServiceAccount (if not exists):
```bash
kubectl create sa testing-sa -n default
```
2. Create a token (example 24h):
```bash
TOKEN=$(kubectl create token testing-sa -n default --duration=24h)
```
3. Store in a Secret and mount it into the Pod:
```bash
kubectl create secret generic testing-sa-token -n default --from-literal=token="$TOKEN"
```
4. Mount the Secret as an env var or file inside the Pod (example `pod-with-manual-token.yaml`).

Option B — Projected `serviceAccountToken` volume (recommended for in-cluster short-lived tokens)
- Request a token explicitly (works even if `automountServiceAccountToken: false`):

```yaml
volumes:
- name: sa-token
	projected:
		sources:
		- serviceAccountToken:
				path: token
				audience: api
				expirationSeconds: 3600
```

Mount it into the container and use the token at `/path/to/token` to authenticate to the API server.

## Example API call from inside the Pod
```bash
TOKEN=$(cat /path/to/token)
curl --cacert /var/run/secrets/kubernetes.io/serviceaccount/ca.crt \
	-H "Authorization: Bearer $TOKEN" \
	https://kubernetes.default.svc/api/v1/namespaces/default/pods
```

## Security notes
- Prefer short-lived, projected tokens for in-cluster workloads.
- If you create a Secret with a token, treat it like any other secret (rotate, restrict RBAC, avoid committing it).
- Minimize ServiceAccount privileges — grant least privilege via RBAC.

## Files in this repo
- Example Pod using a ServiceAccount: `pod-with-service-account.yaml`.
- If you want, I can add `pod-with-manual-token.yaml` and `pod-with-projected-token.yaml` here as examples.

## Tokens for external use
- Sometimes you need a token that an external system (CI, monitoring, backup tool) can use outside the cluster.
- Use `kubectl create token` to mint a token for a ServiceAccount and then store or distribute it securely.

Example:
```bash
# Create serviceaccount (if not already present)
kubectl create sa testing-sa -n default

# Create a token valid for 24 hours and capture it in a variable
TOKEN=$(kubectl create token testing-sa -n default --duration=24h)

# Create a Secret to hold the token (optional) so you can mount it where needed
kubectl create secret generic testing-sa-token -n default --from-literal=token="$TOKEN"
```

Security guidance when giving tokens to external entities:
- Treat the token like any credential — restrict where it is stored and who can read it.
- Use short durations and rotate tokens frequently.
- Limit the ServiceAccount's permissions with RBAC to the minimum required by the external tool.
- Prefer alternative approaches (OIDC client credentials, dedicated CI identity providers) when possible.
