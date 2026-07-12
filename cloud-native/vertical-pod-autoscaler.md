# Vertical Pod Autoscaler

Vertical Pod Autoscaler (VPA) adjusts the CPU and memory requests and limits for a pod based on actual usage.

## Why VPA is needed
If a pod repeatedly reaches its CPU or memory limits, it may become unstable or get killed. VPA helps prevent that by recommending or applying better resource settings.

## Components of VPA
1. Recommender
   - analyzes pod resource usage from the Metrics Server.
   - suggests better CPU and memory requests and limits.

2. Updater
   - checks whether the current pod resource settings differ from the recommendation.
   - applies the changes when needed.

3. Admission Controller
   - helps ensure the updated resource requests and limits are applied correctly.

## Update modes
- Off: VPA only recommends changes; it does not apply them.
- Initial: VPA updates resources only when the pod is first created.
- Auto: VPA updates resources during the pod lifecycle as needed.

## Important note
In newer Kubernetes versions, some resource updates can be applied in place, so the pod may not need to be evicted.

## Quick revision
- VPA changes resource requests and limits.
- It helps prevent resource starvation and instability.
- It works best when resource usage patterns change over time.