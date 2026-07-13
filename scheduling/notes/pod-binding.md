# Pod binding and scheduler behavior

Kubernetes scheduler assigns a Pod to a node by creating a `Binding` object for the Pod.
This is the API-level action that binds the Pod to a specific node.

## Why this is the correct flow
- The scheduler does not directly modify `spec.nodeName` on an existing Pod.
- Instead, it creates a `Binding` object and posts it to the Pod's binding API.
- This mimics the scheduler's behavior in a manual scheduling scenario.

## Binding object example
```yaml
apiVersion: v1
kind: Binding
metadata:
  name: myapp-pod
  namespace: default
target:
  apiVersion: v1
  kind: Node
  name: worker-node-1
```

## API request format
- Endpoint: `POST /api/v1/namespaces/default/pods/myapp-pod/binding`
- Content-Type: `application/json`

### Example curl request
```bash
curl -k -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  --data-binary @binding.json \
  https://<apiserver-host>:6443/api/v1/namespaces/default/pods/myapp-pod/binding
```

Where `binding.json` contains the Binding object.

## Key points
- This is the manual equivalent of scheduler behavior.
- It is used to assign an existing Pod to a specific node.
- It is different from `nodeSelector`, `nodeAffinity`, or directly editing Pod fields.
- Use this API only when you want to emulate scheduler binding explicitly.
