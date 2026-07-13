# ClusterRoles and ClusterRoleBindings

Kubernetes RBAC has both namespace-scoped and cluster-scoped objects.

## Resource scope
- Namespaced resources exist inside a namespace. Examples: `pods`, `replicasets`, `roles`, `rolebindings`, `persistentvolumeclaims`.
- Cluster-scoped resources exist at the cluster level. Examples: `nodes`, `persistentvolumes`, `clusterroles`, `clusterrolebindings`.

## When to use ClusterRole
- Use a `ClusterRole` when you need permissions on cluster-scoped resources.
- Use a `ClusterRole` when you need the same permissions across multiple namespaces.
- A `ClusterRole` can grant access to both cluster-scoped resources and namespaced resources.

## ClusterRole vs Role
- `Role` is namespaced and only controls permissions inside a single namespace.
- `ClusterRole` is cluster-scoped and can apply globally or be bound into namespaces.

## Binding ClusterRoles
- `ClusterRoleBinding` attaches a `ClusterRole` to subjects across the entire cluster.
- `RoleBinding` can also reference a `ClusterRole` to grant its permissions within a specific namespace.

## Example
See [cluster-admin-role.yaml](cluster-admin-role.yaml) for an example ClusterRole that grants wide cluster permissions.

## Notes
- Use `ClusterRole`/`ClusterRoleBinding` for cluster administration and global access.
- For least privilege, prefer `Role`/`RoleBinding` when access is needed only inside one namespace.
- `ClusterRole` is more flexible than `Role` because it can cover both cluster-scoped and namespaced resources.
