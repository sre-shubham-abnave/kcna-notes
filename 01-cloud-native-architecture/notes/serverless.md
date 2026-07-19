# Serverless in Cloud Native Architecture

Serverless is a cloud-native development model that allows developers to build and run applications without having to manage servers. Servers are still used, but the cloud provider or platform abstracts them away, dynamically managing the allocation and provisioning of resources.

---

## Core Characteristics of Serverless

- **Zero Server Management**: Developers do not configure, patch, or scale the underlying host VMs/nodes.
- **Pay-as-you-use (Utility Billing)**: Charges are based on the actual resources consumed by execution (e.g., execution time, memory-seconds) rather than pre-allocated idle capacity.
- **Event-Driven**: Workloads are triggered by events (HTTP requests, database changes, queue messages, file uploads).
- **Scale-to-Zero**: When there is no traffic or active events, the application scales down to zero resources, saving costs and idle resources.
- **High Availability & Fault Tolerance**: Built-in automatically by the underlying serverless platform.

---

## BaaS vs. FaaS

- **BaaS (Backend-as-a-Service)**: Using third-party cloud services for backend logic (e.g., managed databases, authentication services like Auth0, object storage).
- **FaaS (Function-as-a-Service)**: The developer writes modular, single-purpose pieces of code (functions) that run in ephemeral containers triggered by events. **This is the compute model of serverless** (e.g., AWS Lambda, Google Cloud Functions).

---

## Serverless on Kubernetes (Avoiding Vendor Lock-in)

Public cloud serverless services can cause vendor lock-in. Running open-source serverless frameworks on Kubernetes provides **portability**, allowing serverless workloads to run on-premises, in hybrid clouds, or on any cloud provider.

Based on the CNCF Serverless ecosystem, here are the key open-source serverless frameworks and tools:

### 1) Knative (CNCF Graduated Project)
Knative is a Kubernetes-native platform for building, deploying, and managing modern serverless workloads. It abstracts away Kubernetes primitives (like Deployments, Services, and Ingress) to simplify developer workflows.

- **Knative Serving**: Handles deploying and serving of serverless containers.
  - Automatic scaling, including **scale-to-zero** and scaling up from zero.
  - Traffic routing and splitting (useful for canary deployments or A/B testing).
  - Snapshotting of code and configurations (Revisions).
- **Knative Eventing**: Handles event subscription, routing, and delivery.
  - Connects event producers to event consumers (sinks) with loose coupling.
- **Knative Build** (Historical note): Originally handled building source code into container images. It was subsequently deprecated and evolved into the standalone **Tekton** project.

### 2) OpenFaaS (Functions-as-a-Service)
OpenFaaS is a popular, lightweight, developer-friendly framework for hosting functions and microservices on Kubernetes. It packages any containerized process as a function.

- **Gateway**: The RESTful API entry point. It manages functions, routes traffic, handles synchronous invocations, and provides a web dashboard.
- **Queue Worker**: Manages asynchronous requests. It pulls tasks from a message bus (typically NATS) and ensures reliable background execution of functions.
- **Prometheus**: Collects metrics (invocation count, latency, CPU/RAM). The Gateway uses these metrics to scale functions dynamically up and down (via the autoscaler).

### 3) Kubeless (Kubernetes-Native)
Kubeless is an open-source serverless framework built directly on Kubernetes primitives.
- **Kubernetes-Native Design**: It uses Custom Resource Definitions (CRDs) to define functions, and leverages core Kubernetes components (Deployments, Services, ConfigMaps, CronJobs) for executing them.
- Keeps its codebase small and simplifies operations by avoiding duplicate scheduling logic.
- Supports HTTP and event-based triggers for multiple languages (Python, Node.js, Ruby, etc.).

### 4) Fission (Fast & Portable)
Fission is a fast, open-source serverless framework for Kubernetes that focuses on developer productivity and high performance.
- **High Performance (Fast Startups)**: Maintains a pool of warm, idle containers to eliminate "cold start" latency for function execution.
- **Automatic Resource Scaling**: Automatically provisions and scales Kubernetes pods in response to traffic.
- **Provider Agnostic**: Enables easy migration of serverless workloads across any standard Kubernetes cluster.

### 5) Other Mentioned Frameworks
- **Apache OpenWhisk**: A highly mature, distributed serverless platform with a large contributor community. It can be complex to run because it relies on multiple heavy external components (CouchDB, Kafka, Nginx, Redis, Zookeeper) and has historical security design caveats.
- **IronFunctions / Fn / Project Riff**: Alternative container-based serverless environments.

---

## KCNA Exam Takeaway

- **Knative Components**: Remember the division between **Serving** (scale-to-zero, traffic splitting) and **Eventing** (loose coupling via events).
- **Scale-to-Zero**: This is the defining characteristic of a FaaS/Serverless compute system that separates it from standard container deployments.
- **Vendor Lock-in mitigation**: Open-source serverless frameworks (OpenFaaS, Knative, Fission) running on Kubernetes allow workloads to be fully portable.
- **FaaS vs BaaS**: FaaS is developer code run on-demand; BaaS is using third-party managed backend services.

---

## Quick Memory Trick

- **Knative Serving** &rarr; Scales containers up & down (including to zero) and manages routing.
- **Knative Eventing** &rarr; Connects event producers with event consumers.
- **OpenFaaS Gateway** &rarr; API entry point & dashboard.
- **OpenFaaS Queue Worker** &rarr; Handles async background function calls.
- **Fission** &rarr; Warm container pools to prevent cold starts.
- **Kubeless** &rarr; Direct CRD mapping to native Kubernetes primitives.
