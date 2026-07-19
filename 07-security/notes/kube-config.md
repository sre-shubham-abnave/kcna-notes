# kubeconfig

`kubeconfig` files tell `kubectl` how to connect to a cluster: which cluster, which user credentials, and which context to use.

## Main sections
- `clusters`: cluster connection info (server URL, certificate authority).
- `users`: credentials to authenticate (client cert/key, token, exec plugin).
- `contexts`: an association of a user with a cluster and a default namespace.

## Common commands
```bash
# Show the merged kubeconfig the client will use:
kubectl config view

# Use a specific kubeconfig file:
KUBECONFIG=./my-config kubectl get pods
# or
kubectl --kubeconfig=my-custom-config get pods

# Switch context
kubectl config use-context my-cluster-admin@my-cluster
```

## Notes
- Default kubeconfig path: `$HOME/.kube/config`.
- Contexts simplify switching between clusters or users.
- Many auth mechanisms (client certs, tokens, OIDC plugins) are referenced from `users` entries.