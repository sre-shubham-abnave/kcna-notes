# Infrastructure Provisioning & Deployment Approaches

Infrastructure Provisioning refers to the process of setting up and configuring the IT infrastructure (servers, networks, storage, etc.) required to run applications. In cloud-native systems, we categorize deployment and provisioning methodologies into distinct paradigms.

---

## 1. Imperative Deployment Approach (How to do it)

The **imperative approach** involves creating step-by-step instructions to provision an application or infrastructure. You specify the exact commands, actions, and order of operations needed to achieve the target state.

- **Focus**: **HOW** to build/configure the system.
- **Workflow**: Prescriptive list of execution steps. The engineer or script dictates every single instruction.
- **State management**: Mutates the system's state step-by-step. If a step fails, you may end up in a half-configured, inconsistent state.
- **Control**: Provides granular, exact control over the deployment process.
- **Example tools/scenarios**:
  - Bash scripts running a sequence of `docker run` or `apt-get` commands.
  - Using CLI commands sequentially: `kubectl create namespace prod`, `kubectl create deployment web --image=nginx`, etc.
  - Traditional imperative automation (e.g., executing commands via SSH).

---

## 2. Declarative Deployment Approach (What to achieve)

The **declarative approach** defines the desired end-state of the application or infrastructure without specifying the exact steps to reach that state. The system or provisioning tool automatically calculates the delta between the current state and the desired state, and applies the necessary changes.

- **Focus**: **WHAT** the system should look like.
- **Workflow**: Configuration manifest describing the target layout/attributes.
- **State management**: The system constantly reconciles. If there is drift or a failure, the controller/engine works to correct it.
- **Abstraction**: Abstracted complexity; developers do not need to care about the execution commands.
- **Example tools/scenarios**:
  - Kubernetes YAML manifests (`kubectl apply -f deployment.yaml`).
  - Terraform or OpenTofu files (`main.tf`).
  - GitOps tools (Argo CD, Flux).
  - SQL queries (declaring what data to select, not how to retrieve it).

---

## 3. Procedural Deployment Approach

The **procedural approach** involves defining a series of steps or procedures to provision infrastructure.
- **Key details**: While similar to the imperative approach in specifying a sequence, procedural deployment is often less focused on low-level commands and more focused on higher-level execution steps.
- **Control**: May not provide the same granularity of command-level control as a pure imperative approach.

---

## 4. Process-oriented Deployment Approach

The **process-oriented approach** emphasizes the overall workflow, coordination, and interactions between activities and components.
- **Key details**: Rather than describing individual deployment instructions, this approach defines dependencies, state progressions, and interactions between parts of the deployment pipeline.

---

## Comparative Summary Table

| Feature | Imperative | Declarative |
| :--- | :--- | :--- |
| **Primary Question** | **HOW** do I get there? | **WHAT** should it look like? |
| **Instructions** | Step-by-step commands and procedures. | Definition of the desired end-state. |
| **Execution** | Commands executed sequentially. | Controller evaluates drift and reconciles. |
| **Complexity** | User manages control flow and order of operations. | User delegates control flow to the engine/tool. |
| **Examples** | Bash scripts, Ansible tasks (imperative modules), CLI. | Kubernetes YAML manifests, Terraform, CloudFormation. |

---

## KCNA Exam Takeaway

> [!IMPORTANT]
> If a question asks:
> - *“What type of deployment approach involves the creation of step-by-step instructions to provision an application or infrastructure?”*
>
> The correct answer is: **imperative**.
>
> - **Imperative vs. Declarative**: Remember, **imperative** is *instructions* (how to do it), and **declarative** is *configuration/end-state* (what to do).
> - **GitOps connection**: GitOps operates entirely on the **declarative** model. Declarative configurations are version-controlled in Git, and pull-based operators continuously reconcile the state.

---

## Quick Memory Trick

- **Imperative** &rarr; *"Recipe steps"*: Pre-heat oven, stir flour, mix eggs, bake (Instructions).
- **Declarative** &rarr; *"Order a cake"*: I want a chocolate cake with frosting (End-state).
- **Procedural** &rarr; High-level procedures/runs.
- **Process-oriented** &rarr; Workflow/coordination.
