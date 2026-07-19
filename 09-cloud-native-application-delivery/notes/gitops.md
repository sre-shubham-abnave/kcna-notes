# GitOps and OpenGitOps

GitOps is a set of practices to manage infrastructure and application configurations using Git as the single source of truth. It uses declarative specifications to define the desired state of a system and software agents to reconcile the actual state with this desired state.

The **GitOps Working Group** is a working group under the CNCF **TAG App Delivery** (Technical Advisory Group, formerly SIG App Delivery).

---

## The OpenGitOps Project

**OpenGitOps** is an open-source project hosted under the CNCF, initiated by the GitOps Working Group.

### Primary Purpose:
- **Define and standardize best practices** for GitOps.
- **Create a common language and understanding** of GitOps that is accessible and usable by everyone (vendors, end-users, and open-source contributors).
- Foster collaboration and interoperability across different teams and organizations.

### Key Clarifications for the KCNA Exam:
> [!IMPORTANT]
> - **Not specific to Kubernetes**: Although GitOps is highly popular in the Kubernetes ecosystem, the OpenGitOps principles are generic and apply to non-Kubernetes systems as well.
> - **Not about developing new tools**: The project does not aim to build new GitOps tools (like Argo CD or Flux), but rather to standardize principles and patterns.
> - **Not about reducing Kubernetes components**: It does not aim to simplify Kubernetes core architecture or reduce its component count.
> - **Not about integrating Kubernetes**: Its primary goal is not to integrate Kubernetes with existing/future market tools, but to define a common methodology.

---

## The Four Core Principles of GitOps (OpenGitOps v1.0)

For a system to be considered "GitOps compliant," it must follow these four principles:

### 1) Declarative
The desired state of the entire system must be expressed declaratively (e.g., using YAML or JSON manifest files).
- *Exam takeaway*: The configuration describes *what* the system should look like, not *how* to achieve it.

### 2) Versioned and Immutable
The desired state is stored in a version control system (typically Git) that enforces immutability, versioning, and keeps a complete, auditable version history.
- *Exam takeaway*: Every state change is tracked, allowing easy rollbacks and historical audit trails.

### 3) Pulled Automatically
Software agents automatically pull the desired state declarations from the source repository once approved changes are detected.
- *Exam takeaway*: The system updates itself automatically based on changes in Git.

### 4) Continuously Reconciled
Software agents continuously observe the actual state of the system and compare it to the desired state. If divergence (configuration drift) occurs, the agent automatically attempts to reconcile and align the actual state with the desired state.
- *Exam takeaway*: Detects and corrects "drift" automatically without manual intervention.

---

## Push-based vs. Pull-based GitOps

### Push-based Deployment
- The CI/CD pipeline (e.g., GitHub Actions, GitLab CI) triggers a script or command to push changes to the target cluster.
- **Drawback / Security Risk**: The external pipeline needs administrative credentials (like `kubeconfig`) to access the cluster. If the CI/CD pipeline is compromised, the cluster credentials are exposed.

### Pull-based Deployment
- A software agent (operator) runs directly inside the target cluster (e.g., Argo CD, Flux CD).
- The agent polls the Git repository for changes. When a change is detected, it pulls the manifests and applies them locally.
- **Benefit / Security Advantage**: Credentials never leave the cluster boundaries. No external system needs administrative access to the Kubernetes cluster.

---

## Example GitOps Operators in Kubernetes
- **Argo CD**: Uses a pull-based model, runs inside Kubernetes, monitors Git repos, and has a rich UI for managing application states.
- **Flux CD**: A lightweight, highly modular CNCF graduated GitOps toolkit.

---

## KCNA Exam Takeaway

- **OpenGitOps Goal**: Create a shared language and define/standardize GitOps best practices.
- **GitOps WG**: Belongs to CNCF **TAG App Delivery**.
- **Security**: Pull-based GitOps is more secure because cluster credentials do not need to be shared with external CI/CD pipelines.
- **Reconciliation**: The continuous loop of checking desired state vs. actual state and correcting drift is called reconciliation.

---

## Quick Memory Trick

- **Declarative** &rarr; *What* the system should look like.
- **Versioned & Immutable** &rarr; History stored in Git.
- **Pulled Automatically** &rarr; Agent polls and downloads config.
- **Continuously Reconciled** &rarr; Agent heals drift automatically.