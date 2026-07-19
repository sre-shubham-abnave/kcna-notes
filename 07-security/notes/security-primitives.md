# Security primitives in Kubernetes

The `kube-apiserver` is the central control plane component and the main attack surface. Securing access to the API server is the first line of defense.

## Core concepts
- **Authentication** — who is making the request (users, service accounts, system components).
- **Authorization** — whether that identity is allowed to perform the requested action (RBAC, ABAC, webhook).
- **Admission controllers** — plugins that can mutate or validate objects after authorization (e.g., `PodSecurity`, `ResourceQuota`, `LimitRanger`).

## Common controls
- **RBAC** (Role-Based Access Control) — define Roles and RoleBindings or ClusterRoles and ClusterRoleBindings.
- **ServiceAccounts** — identities for Pods; use them for in-cluster workloads.
- **Network policies** — control traffic between Pods.
- **TLS / certificates** — secure API and component communication.

## Notes for KCNA
- Understand the difference between authentication and authorization.
- Know basic RBAC objects: `Role`, `ClusterRole`, `RoleBinding`, `ClusterRoleBinding`.
- Admission controllers are where cluster policies are enforced before objects are persisted.