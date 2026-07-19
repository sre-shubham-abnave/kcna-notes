# Multiple Schedulers in Kubernetes

By default, Kubernetes uses a built-in scheduler called `default-scheduler` (`kube-scheduler`) to place Pods onto Nodes. However, you can write and run your own **custom schedulers** alongside the default one. 

This note covers how the default and custom schedulers work together, how they differ, and what you need to know for the KCNA exam.

---

## 1. Default Scheduler (`kube-scheduler`)

The default scheduler is a core control plane component that watches for newly created Pods that have no Node assigned. For every Pod it discovers, it determines the best Node for it to run on.

### The Two-Stage Scheduling Cycle:
1. **Filtering (Predicates)**:
   - Evaluates nodes to find the set of nodes that are capable of running the Pod.
   - Runs checks like: Are there enough CPU/memory resources? Does the node match the `nodeSelector`? Does the node have a taint that the pod does not tolerate?
   - Nodes that do not meet these criteria are filtered out.
2. **Scoring (Priorities)**:
   - Ranks the remaining nodes to find the most suitable placement.
   - Scores each node on a scale (0 to 100) using active priority rules (e.g., node resource balance, image locality, affinity matching).
   - The node with the highest score is chosen. If there is a tie, it selects one randomly.

Finally, the scheduler performs **Binding**: it informs the API server of its decision by creating a binding resource linking the Pod to the chosen Node.

---

## 2. Custom Schedulers

You can run one or more custom schedulers in your Kubernetes cluster. A custom scheduler can be written in any language (Go, Python, etc.) and typically runs as a Deployment inside the cluster.

### Why use a Custom Scheduler?
- **Specialized Workloads**: When you need scheduling logic not supported by default (e.g., gang scheduling for batch jobs, scheduling based on hardware temperatures, or external load balancer metrics).
- **Custom Algorithms**: Round-robin scheduling, random assignment, or priority queues tailored to specific business logic.

---

## 3. How Multiple Schedulers Work Together

Kubernetes supports running multiple schedulers concurrently. They do not interfere with each other because they only act on Pods assigned to them.

- **Unique Identification**: Every scheduler running in the cluster must have a **unique name** (e.g., `default-scheduler`, `my-custom-scheduler`).
- **Targeted Selection**: Schedulers look at the `spec.schedulerName` field of Pod manifests to decide which Pods to process:
  - If `spec.schedulerName` is omitted, it defaults to `default-scheduler`.
  - Schedulers ignore any Pod whose `schedulerName` does not match their own configured name.
  - If a Pod requests a scheduler that is not running in the cluster, the Pod will remain in a **Pending** state indefinitely.

---

## 🛠️ Pod Manifest Example

Below is an example of a Pod configured to use a custom scheduler:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-custom-scheduled-pod
  labels:
    app: web
spec:
  schedulerName: my-custom-scheduler # <-- Tells the default scheduler to ignore this Pod
  containers:
  - name: nginx-container
    image: nginx
```

---

## 📊 Comparison Summary

| Feature | Default Scheduler (`kube-scheduler`) | Custom Scheduler |
| :--- | :--- | :--- |
| **Role** | Standard scheduling engine for the cluster. | Supplemental engine for custom scheduling needs. |
| **Placement** | Runs as part of the core Control Plane. | Runs as a Pod (Deployment/DaemonSet) in user-space. |
| **Default Selection** | Processes any Pod without a defined `schedulerName`. | Processes only Pods explicitly requesting its name. |
| **Logic** | Standard Filtering (Predicates) and Scoring (Priorities). | Custom code logic (e.g., batching, round-robin). |

---

## 🎯 KCNA Exam Takeaway

> [!IMPORTANT]
> - **Unique Names**: Each scheduler running in the cluster must have a unique identifier name.
> - **Pod Configuration**: The field used to choose a scheduler in a Pod manifest is **`spec.schedulerName`**.
> - **Coexistence**: Yes, multiple schedulers can run simultaneously. They ignore Pods that do not match their name.
> - **Pending State**: If a Pod specifies a non-existent `schedulerName`, it stays **Pending** forever.
> - **Scheduling Steps**: Remember the two main steps: **Filtering** (finding fit nodes) and **Scoring** (ranking them).