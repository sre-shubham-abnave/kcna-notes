Authorization controls what an authenticated identity (user, service account, or component) is allowed to do in the cluster.

## Why authorization matters
- Authentication proves who you are. Authorization determines what that identity can do (for example, list Pods, create Deployments, delete Namespaces).

## Built-in authorizers
- **AlwaysAllow / AlwaysDeny** — very simple modes for testing (AlwaysAllow grants everything; AlwaysDeny denies everything).
- **Node** — grants kubelets limited permissions tied to their node identity (e.g., update status of Pods running on that node, read/write their Node object). Use this to allow node components to manage workloads they own.
- **RBAC** (Role-Based Access Control) — the standard, recommended mechanism for production. Defines `Role`/`ClusterRole` and `RoleBinding`/`ClusterRoleBinding` to grant verbs (get, list, watch, create, update, delete) on resources.
- **ABAC** (Attribute-Based Access Control) — legacy file-based policy; rarely used and generally deprecated in favor of RBAC.
- **Webhook** — an external HTTP service is called to make authorize/deny decisions. Useful for integrating custom or centralized authorization systems.

## RBAC basics
- `Role` (namespaced) / `ClusterRole` (cluster-wide) specify a set of permissions (verbs, resources, apiGroups).
- `RoleBinding` and `ClusterRoleBinding` attach roles to subjects (users, groups, serviceAccounts).

Example: a namespaced Role and RoleBinding granting read-only access to Pods
```yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
	name: pod-reader
	namespace: my-namespace
rules:
	- apiGroups: [""]
		resources: ["pods"]
		verbs: ["get", "list", "watch"]

---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
	name: bind-pod-reader
	namespace: my-namespace
subjects:
	- kind: User
		name: alice
roleRef:
	kind: Role
	name: pod-reader
	apiGroup: rbac.authorization.k8s.io
```

## Configuring authorization
- `--authorization-mode` on `kube-apiserver` sets which authorizers are enabled (comma-separated list). Common value: `Node,RBAC`.
- The request is evaluated by the enabled authorizers; if any authorizer allows the action, the request succeeds (subject to admission controllers).

## Notes for KCNA
- Know the RBAC objects: `Role`, `ClusterRole`, `RoleBinding`, `ClusterRoleBinding`.
- Understand the Node authorizer purpose (kubelet/node permissions) vs RBAC for user/service-account permissions.
- Webhook authorizers delegate decisions to external services — useful in enterprise integrations.
