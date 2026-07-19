# RBAC (Role-Based Access Control)

RBAC in Kubernetes grants permissions by associating subjects (users, service accounts) with roles that define what actions they can perform.

## Important: Users are NOT Kubernetes objects
- When you create a `RoleBinding` with a user subject (e.g., `dev-user`), you are **not** creating the user.
- You are creating an **authorization policy** that says: "if someone authenticates as `dev-user`, grant this role."
- The user must be created separately via authentication mechanisms (client certificates, token files, OIDC, etc.).

## RBAC objects
- **Role** (namespaced) — defines permissions within a namespace.
- **ClusterRole** (cluster-wide) — defines permissions across the entire cluster.
- **RoleBinding** (namespaced) — attaches a Role to subjects within a namespace.
- **ClusterRoleBinding** (cluster-wide) — attaches a ClusterRole to subjects across the cluster.

## Namespaced RBAC — what does it mean?
When `Role` and `RoleBinding` are **namespaced**, it means:

1. **Scope** — a Role and RoleBinding belong to a specific namespace. You must specify the namespace (metadata.namespace) when creating them, or they default to the active namespace in your kubeconfig.

2. **Permissions are namespace-local** — a Role in namespace `production` only controls access to resources within `production`. A Role in namespace `development` does not affect permissions in `production`.

3. **Example**: 
   - Role in namespace `dev`: allows creating Pods — grants permission to create Pods **only** in the `dev` namespace.
   - User with this RoleBinding in `dev` cannot create Pods in `production` (a separate namespace).

4. **Contrast with ClusterRole/ClusterRoleBinding** — these are cluster-wide and not scoped to any namespace. A ClusterRole can define permissions across all namespaces (e.g., read all Pods everywhere).

For example:
```bash
# Show Roles in the current namespace
kubectl get roles

# Show Roles in a specific namespace
kubectl get roles -n production

# Create a Role in a specific namespace
kubectl create -f role.yaml -n production
```

This design allows multi-tenant clusters where each team has a namespace and its own RBAC policies.

## Rule syntax
Each rule in a role specifies:
- `apiGroups` — API groups (e.g., `""` for core, `"apps"` for deployments, `"batch"` for jobs).
- `resources` — resource types (e.g., `"pods"`, `"deployments"`, `"configmaps"`).
- `verbs` — actions allowed (e.g., `"get"`, `"list"`, `"create"`, `"update"`, `"delete"`, `"watch"`).
- `resourceNames` (optional) — restrict to specific resource instances (e.g., only allow access to a specific Pod by name).

## Example Role
See [developer-role.yaml](developer-role.yaml) for a namespaced Role that grants permissions to create, list, get, update, and delete Pods and create ConfigMaps.

## Example RoleBinding
See [devuser-developer-rolebinding.yaml](devuser-developer-rolebinding.yaml) for an example RoleBinding that grants the Developer role to the user `dev-user`.

To test permissions:
```bash
# Check if current user can create pods
kubectl auth can-i create pods

# Check if dev-user can create pods
kubectl auth can-i create pods --as dev-user
```

## Common patterns
- Use `Role` + `RoleBinding` for isolated namespaces (e.g., one team per namespace).
- Use `ClusterRole` + `ClusterRoleBinding` for cluster-wide permissions (e.g., cluster admins).
- Use the `system:` prefix for system-managed accounts and roles.

## Notes for KCNA
- Understand the difference between authentication (who you are) and authorization (what you can do).
- Know the four RBAC objects and when to use namespace-scoped vs cluster-scoped versions.
- Remember: users must authenticate first (via certs, tokens, etc.); RoleBindings grant them permissions after authentication.

