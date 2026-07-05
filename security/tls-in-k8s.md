TLS in Kubernetes

Kubernetes components use TLS for authentication and encryption. A cluster typically has a CA (certificate authority) that signs component and client certificates.

## Quick example (openssl)
Generate a CA key and certificate signing request, then self-sign a CA certificate (demo only):

```bash
openssl genrsa -out ca.key 2048
openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr
openssl x509 -req -in ca.csr -signkey ca.key -days 365 -out ca.crt
```

## Notes and best practices
- Use Subject Alternative Names (SANs) for server certificates (APIServer needs DNS/IP SANs).
- Kubeadm automates much of certificate generation and rotation for production clusters; prefer that over manual openssl workflows.
- Components that commonly need certificates: API server, kubelet (client and server certs), kube-proxy, controller-manager, scheduler.
- Distribute CA and client certs securely; rotate keys periodically.
