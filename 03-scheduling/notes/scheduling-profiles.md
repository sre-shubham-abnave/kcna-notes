# Scheduling Profiles in Kubernetes

Scheduling profiles are a way to define different scheduling behaviors for different workloads using the same Kubernetes scheduler. They are especially useful when you want to tune how pods are placed on nodes without creating a completely separate scheduler process.

For the KCNA exam, focus on this idea:
- A scheduler profile is a named scheduling strategy.
- Kubernetes uses the profile that matches the pod’s scheduler name.
- Profiles help customize the scheduling logic by enabling or disabling plugins and changing their behavior.

---

## 1. Core idea: what is a scheduling profile?

A Kubernetes scheduler does not just “pick any node.” It follows a structured decision process.

The basic flow is:
1. **Queueing**: Pods waiting to be scheduled enter the scheduling queue.
2. **Filtering**: The scheduler removes nodes that cannot run the pod.
3. **Scoring**: The remaining nodes are ranked based on suitability.
4. **Binding**: The best node is chosen and the pod is attached to it.

A scheduling profile controls how this process works for a specific group of pods.

---

## 2. Why scheduling profiles are useful

Different workloads may need different scheduling rules.

Examples:
- A batch workload may need strict resource placement.
- A latency-sensitive workload may prefer nodes with better locality or available resources.
- A special workload may need custom plugin behavior.

Instead of changing one global scheduling strategy for everything, Kubernetes allows you to define multiple profiles and use them depending on the pod’s configuration.

---

## 3. How profiles work

The scheduler reads the pod’s `spec.schedulerName` field.

- If the pod does not specify a scheduler name, it uses the default scheduler.
- If a profile exists for that scheduler name, the scheduler uses that profile.
- If no matching profile is found, the pod is handled by the default behavior.

This means scheduling profiles are closely related to the concept of scheduler selection.

---

## 4. Important scheduling phases

Remember this sequence for exams:

- **Queue sort**: Pods are ordered in the scheduling queue.
- **Filtering**: Unsuitable nodes are removed.
- **Scoring**: Remaining nodes are ranked.
- **Binding**: The chosen node is assigned to the pod.

A simple way to remember it is:

Queue -> Filter -> Score -> Bind

---

## 5. Priority and scheduling order

Pods in the queue are often sorted by priority.

- A **PriorityClass** can be used to assign priority to pods.
- A higher priority value means the pod is considered more important.
- This affects scheduling order, especially when many pods compete for resources.

So, in simple terms:
- Priority helps decide which pod gets attention first.
- Scheduling profiles help decide how the scheduler evaluates nodes for that pod.

---

## 6. Example configuration

A scheduling profile is defined inside a scheduler configuration file using `KubeSchedulerConfiguration`.

```yaml
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profiles:
  - schedulerName: my-scheduler
    plugins:
      queueSort:
        enabled:
          - name: PrioritySort
      filter:
        enabled:
          - name: NodeResourcesFit
      score:
        enabled:
          - name: NodeResourcesFit
          - name: ImageLocality
```

This example shows that the profile `my-scheduler` uses a specific set of scheduling plugins.

---

## 7. Difference between scheduling profiles and multiple schedulers

This is a common exam confusion.

- **Scheduling profiles** are different scheduling strategies inside the scheduler configuration.
- **Multiple schedulers** means more than one scheduler process running in the cluster.

In short:
- Profiles customize behavior.
- Multiple schedulers provide separate scheduling engines.

### Quick exam observation

This is one of the ultimate trick questions on Kubernetes exams. The short answer is: you use the exact same property, `spec.schedulerName`.

- For a **scheduling profile**, the pod uses `spec.schedulerName` to match a profile name defined inside the default scheduler configuration.
- For **multiple schedulers**, the pod uses `spec.schedulerName` to match the name of a separate scheduler process.

So the pod does not care how the scheduler is implemented. It only leaves a name in `spec.schedulerName` and waits for whichever scheduler process claims that name.

---

## 8. KCNA exam takeaway

Remember these points:
- Scheduling profiles let you define different scheduling behavior for different pods.
- They are configured through `KubeSchedulerConfiguration`.
- The profile is selected using the pod’s `spec.schedulerName`.
- The scheduler still follows the same core flow: **queue → filter → score → bind**.
- Priority classes influence scheduling order, while profiles influence scheduling strategy.

> Key exam idea: scheduling profiles help customize how the scheduler places pods, but the fundamental scheduling process remains the same.
