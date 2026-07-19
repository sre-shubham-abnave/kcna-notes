# KCNA Study Guide & Master Index

Welcome! This repository contains study notes prepared for the **Kubernetes and Cloud Native Associate (KCNA)** exam. The notes are organized in folders numbered sequentially (`01-*` to `09-*`) following the recommended learning path from the [KodeKloud KCNA Course](https://learn.kodekloud.com/user/courses/kubernetes-and-cloud-native-associate-kcna) and the official CNCF exam curriculum.

---

## 🗺️ Master Study Path

Follow this order to study for your exam:

### 📂 01. Cloud Native Architecture
Covers the core concepts of cloud-native computing, container standards, scaling, and serverless compute frameworks.
1. 📝 **[Cloud Native Fundamentals](./01-cloud-native-architecture/notes/cloud-native-fundamentals.md)** &mdash; Definitions of cloud-native, microservices, orchestration, automation, and core architecture tenets.
2. 📝 **[Open Container Initiative (OCI)](./01-cloud-native-architecture/notes/open-container-initiative.md)** &mdash; OCI standards: `image-spec`, `runtime-spec`, and `distribution-spec`.
3. 📝 **[Kubernetes Open Standards](./01-cloud-native-architecture/notes/kuberntes-open-standards.md)** &mdash; Extensibility standards (CRI, CNI, CSI, and SMI).
4. 📝 **[Horizontal Pod Autoscaler (HPA)](./01-cloud-native-architecture/notes/horizontal-pod-autoscaler.md)** &mdash; Dynamic scaling based on CPU, memory, or custom metrics.
5. 📝 **[Vertical Pod Autoscaler (VPA)](./01-cloud-native-architecture/notes/vertical-pod-autoscaler.md)** &mdash; Automatically adjusting resource requests/limits of existing containers.
6. 📝 **[Serverless](./01-cloud-native-architecture/notes/serverless.md)** &mdash; Serverless definition, FaaS vs. BaaS, and open-source frameworks (Knative, OpenFaaS, Kubeless, Fission).

---

### 📂 02. Kubernetes Resources & Basics
Foundations of working with core API resources, configuration approaches, and utilizing `kubectl`.
1. 📝 **[Imperative vs. Declarative Config](./02-kubernetes-resources/notes/imperative-vs-declartive.md)** &mdash; Core concepts of defining configurations (imperative commands vs. declarative configurations).
2. 📝 **[Kubectl Explain](./02-kubernetes-resources/notes/kubectl-explain.md)** &mdash; Using `kubectl explain` to explore resource schemas and documentation from the command line.
3. 📝 **[Kubectl Apply](./02-kubernetes-resources/notes/kubectl-apply.md)** &mdash; The declarative workflow using `kubectl apply` and configuration drift.
4. 📝 **[Deployment Notes](./02-kubernetes-resources/notes/deployment-notes.md)** &mdash; Core Kubernetes resources, controller manager loop, and managing rollouts/rollbacks.

---

### 📂 03. Kubernetes Scheduling
Rules, constraints, and workloads that determine how and where Pods are placed onto cluster Nodes.
1. 📝 **[Labels & Selectors](./03-scheduling/notes/labels-selectors.md)** &mdash; Organizing and selecting subsets of objects (Pods, Nodes).
2. 📝 **[Manual Scheduling](./03-scheduling/notes/manual-scheduling.md)** &mdash; Scheduling a Pod manually by directly configuring the `nodeName` property.
3. 📝 **[Pod Binding](./03-scheduling/notes/pod-binding.md)** &mdash; How Pods bind to Nodes behind the scenes using binding resources.
4. 📝 **[Resource Requirements](./03-scheduling/notes/resource-requirements.md)** &mdash; Pod resource requests (scheduling floor) and limits (throttling/OOM ceilings).
5. 📝 **[Node Selectors](./03-scheduling/notes/node-selectors.md)** &mdash; Simplest node constraints (`nodeSelector` targeting node labels).
6. 📝 **[Node Affinity](./03-scheduling/notes/node-affinity.md)** &mdash; Advanced scheduling constraints (soft/hard affinity, expression matching).
7. 📝 **[Taints & Tolerations](./03-scheduling/notes/taints-and-tolerations.md)** &mdash; Restricting nodes from accepting certain pods (taints) and allowing pods to bypass restrictions (tolerations).
8. 📝 **[Topology Spread Constraints](./03-scheduling/notes/spread-constraints.md)** &mdash; Distributing Pods evenly across failure domains (zones, regions).
9. 📝 **[DaemonSets](./03-scheduling/notes/daemonsets.md)** &mdash; Running a single pod on every single node (e.g., logging/monitoring agents).
10. 📝 **[Static Pods](./03-scheduling/notes/static-pods.md)** &mdash; Local kubelet-managed pods in `/etc/kubernetes/manifests` bypassing the API server.
11. 📝 **[Multiple Schedulers](./03-scheduling/notes/multiple-scheduler.md)** &mdash; Configuring and executing custom schedulers in the same cluster.
12. 📝 **[Scheduling Profiles](./03-scheduling/notes/scheduling-profiles.md)** &mdash; Custom scheduling pipelines (queueing, filtering, scoring).

---

### 📂 04. Kubernetes Networking
The networking requirements of a Kubernetes cluster, how Pods communicate, DNS resolution, and exposing services.
1. 📝 **[Container Network Interface (CNI)](./04-networking/notes/container-network-interface.md)** &mdash; CNI standard, specifications, and pluggable network architectures.
2. 📝 **[Cluster Networking](./04-networking/notes/cluster-networking.md)** &mdash; Port requirements, control-plane communication, and host-level interfaces.
3. 📝 **[Pod Networking](./04-networking/notes/pod-networking.md)** &mdash; IP-per-Pod network requirements and the virtual ethernet interfaces (`veth`).
4. 📝 **[DNS in Kubernetes](./04-networking/notes/dns.md)** &mdash; Service name resolution, CoreDNS deployment, and domain formats.
5. 📝 **[Ingress](./04-networking/notes/ingress.md)** &mdash; Exposing HTTP/HTTPS routes from outside the cluster to services within the cluster using Ingress resources and controllers.

---

### 📂 05. Services & Service Mesh
Native Kubernetes Service types, the concept of a service mesh, sidecar proxies, and mesh controllers.
1. 📝 **[Kubernetes Services](./05-services/notes/k8s-services.md)** &mdash; Core service primitives: ClusterIP, NodePort, LoadBalancer, and ExternalName.
2. 📝 **[Service Mesh Fundamentals](./05-services/notes/service-mesh.md)** &mdash; What a service mesh is, why it is used (mTLS, traffic control, observability), and SMI (Service Mesh Interface).
3. 📝 **[Sidecars](./05-services/notes/sidecars.md)** &mdash; The sidecar container design pattern for transparent traffic routing.
4. 📝 **[Envoy Proxy](./05-services/notes/envoy.md)** &mdash; Envoy proxy as the popular high-performance data plane for service meshes.
5. 📝 **[Istio](./05-services/notes/istio.md)** &mdash; Istio architecture (Control Plane - `istiod`, and Data Plane - Envoy).

---

### 📂 06. Kubernetes Storage
Concepts of block/file storage integration, storage plug-ins, and dynamic volume allocation.
1. 📝 **[Container Storage Interface (CSI)](./06-storage/notes/container-storage-interface.md)** &mdash; CSI standards, decoupling storage backends from Kubernetes core codebase.
2. 📝 **[Storage Drivers](./06-storage/notes/storage-drivers.md)** &mdash; Overview of driver-level storage integration in container platforms.
3. 📝 **[Volume Drivers](./06-storage/notes/volume-drivers.md)** &mdash; Plugins and libraries allowing containers to connect to third-party storage.
4. 📝 **[Volumes in Kubernetes](./06-storage/notes/volumes-in-k8s.md)** &mdash; Ephemeral volume mounts tied to pod lifecycles (e.g., `emptyDir`, `hostPath`).
5. 📝 **[Persistent Volumes & Claims (PV/PVC)](./06-storage/notes/pv-pvc.md)** &mdash; Persistent volume lifecycles, static provisioning, and binding claims.
6. 📝 **[Storage Classes](./06-storage/notes/storage-class.md)** &mdash; Dynamic provisioning of Persistent Volumes on-demand using storage provisioners.

---

### 📂 07. Kubernetes Security
Security primitives of a Kubernetes cluster, authorization mechanics, certificates, and access control.
1. 📝 **[Security Primitives](./07-security/notes/security-primitives.md)** &mdash; High-level security concepts and the "4C's of Cloud Native Security" (Cloud, Cluster, Container, Code).
2. 📝 **[Kubernetes API Server Security](./07-security/notes/k8s-api.md)** &mdash; Securing access to the API server, transport security, and endpoints.
3. 📝 **[TLS in Kubernetes](./07-security/notes/tls-in-k8s.md)** &mdash; Certificates, Public Key Infrastructure (PKI), and internal cluster communications.
4. 📝 **[Kubeconfig](./07-security/notes/kube-config.md)** &mdash; Organizing connection information (clusters, users, contexts) for administrators and users.
5. 📝 **[Authentication](./07-security/notes/authentication.md)** &mdash; Identity verification (X.509 client certs, HTTP basic auth, tokens, OIDC).
6. 📝 **[Authorization](./07-security/notes/authorization.md)** &mdash; Determining request permissions (RBAC, ABAC, Node, Webhook modules).
7. 📝 **[Role-Based Access Control (RBAC)](./07-security/notes/rbac.md)** &mdash; Defining namespaced resource permissions using `Role` and `RoleBinding`.
8. 📝 **[Cluster Roles](./07-security/notes/cluster-roles.md)** &mdash; Defining cluster-wide permissions using `ClusterRole` and `ClusterRoleBinding`.
9. 📝 **[Service Accounts](./07-security/notes/service-account.md)** &mdash; Pod identities and secure communication between workloads and the API server.

---

### 📂 08. Cloud Native Observability
Fundamentals of cloud-native observability, metrics collection, service level standards, and Prometheus architecture.
1. 📝 **[Observability Fundamentals](./08-observability/notes/observability-fundamentals.md)** &mdash; The three pillars of observability: Metrics, Logs, and Traces.
2. 📝 **[SLOs, SLAs, and SLIs](./08-observability/notes/slo-sla-sli.md)** &mdash; Formulating service level expectations (Indicators, Objectives, and Agreements).
3. 📝 **[Container Metrics](./08-observability/notes/container-metrics.md)** &mdash; Kubernetes cluster metrics exporters (metrics-server, kube-state-metrics).
4. 📝 **[Prometheus Architecture](./08-observability/notes/prometheus-architecture.md)** &mdash; Scrape loop, TSDB (Time Series Database), Pushgateway, Alertmanager, and dashboards.
5. 📝 **[Prometheus Basics](./08-observability/notes/prometheus-basics.md)** &mdash; Prometheus operation, data types, and scraping configuration.
6. 📝 **[Prometheus Metrics Types](./08-observability/notes/prometheus-metrics.md)** &mdash; Time-series metric categories: Counter, Gauge, Histogram, and Summary.
7. 📝 **[Prometheus Monitoring in Kubernetes](./08-observability/notes/prometheus-monitroing-kubernets.md)** &mdash; Configuring Prometheus to scrape Kubernetes API server, Kubelet, and target Pod endpoints.

---

### 📂 09. Cloud Native Application Delivery
GitOps methodologies, provisioning approaches, and delivery patterns for cloud-native systems.
1. 📝 **[Infrastructure Provisioning](./09-cloud-native-application-delivery/notes/infrastructure-provisioning.md)** &mdash; Imperative vs. Declarative provisioning approaches, procedural vs. process-oriented models.
2. 📝 **[GitOps](./09-cloud-native-application-delivery/notes/gitops.md)** &mdash; GitOps definition, the OpenGitOps project (standardizing practices), the 4 Core Principles of GitOps, and push vs. pull deployment.

---

## 🎓 CNCF KCNA Exam Domain Weightings
- **Kubernetes Fundamentals**: 46% (Covered in Modules 2, 3, 4, 5, 6)
- **Container Orchestration**: 22% (Covered in Modules 1, 4, 6)
- **Cloud Native Architecture**: 16% (Covered in Module 1)
- **Cloud Native Observability**: 8% (Covered in Module 8)
- **Cloud Native Application Delivery**: 8% (Covered in Module 9)
