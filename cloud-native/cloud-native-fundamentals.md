# Cloud Native Fundamentals

Cloud-native means building and running applications in a way that fully uses the power of modern cloud platforms.

## Core idea
Cloud-native applications are designed for:
- scalability
- resilience
- faster delivery
- automation
- portability

## Main principles
1. Containers
   - Package the application and its dependencies together.
   - Make deployments portable and consistent.

2. Orchestration
   - Kubernetes schedules, scales, and manages containers.
   - It handles self-healing, rolling updates, and service discovery.

3. Microservices
   - Break a large monolith into smaller, independent services.
   - Improves fault isolation but adds complexity.

4. Automation
   - Use CI/CD pipelines to build, test, and deploy quickly.
   - Infrastructure should be managed as code.

5. Observability
   - Applications and infrastructure must be easy to monitor and troubleshoot.

6. Security by design
   - Use RBAC, secrets, image scanning, and network policies.

## Key Kubernetes concepts
- Pod: the smallest deployable unit.
- Deployment: manages rolling updates and replica count.
- Service: provides stable networking to pods.
- ConfigMap: stores non-sensitive configuration.
- Secret: stores sensitive values.
- Ingress: exposes services externally.
- Namespace: logical separation of resources.
- HPA: scales pods automatically based on CPU or custom metrics.

## Why cloud-native matters
- Faster releases
- Better resource efficiency
- Higher availability
- Easier scaling
- Better developer productivity

## Interview-friendly summary
Cloud-native is not just about running applications on the cloud. It is about building systems that are automated, resilient, observable, and scalable from the start.
