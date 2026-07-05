# Authentication in Kubernetes

Clients that call the `kube-apiserver` must be authenticated before the API server will process requests.

## Who accesses the cluster
- Human users (admins, developers)
- Machine users (bots, CI systems)
- System components (kubelets, controllers)

## Authentication methods
- Client certificates (TLS client certs): the API server validates certificates presented by clients.
- Static token file: simple bearer tokens defined in a file on the API server (useful for demos, not recommended for production).
- ServiceAccount tokens: automatically mounted into Pods; validated by the API server.
- OpenID Connect (OIDC) / external identity providers: integrate with IdPs (e.g., Google, Azure AD).
- Authentication webhooks: delegate authentication to an external service.

## Authentication flow
1. Client presents credentials (client cert, token, etc.).
2. API server verifies the credentials using configured authenticators.
3. If authentication succeeds, the request proceeds to authorization (RBAC, ABAC, etc.).

## Notes
- Authentication only establishes the identity of the caller. Authorization determines what that identity can do.
- Prefer strong, centrally managed identity providers (OIDC) in production.



