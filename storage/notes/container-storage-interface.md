# Container Storage Interface (CSI)

## Why CSI exists
Kubernetes needs a common way to work with different storage backends. CSI provides that standard interface.

## Analogy
- CRI: standard for container runtimes.
- CNI: standard for networking plugins.
- CSI: standard for storage plugins.

## What CSI does
CSI allows Kubernetes to integrate with many storage vendors such as:
- Portworx
- Amazon EBS
- Azure Disk / Azure File
- Dell EMC
- GlusterFS

## Important idea
CSI is not limited to Kubernetes. It is a universal standard that can be used by different container orchestration platforms.

## Exam points
- CSI enables pluggable storage solutions.
- Storage vendors provide CSI drivers.
- Kubernetes uses the CSI driver to provision and attach storage.
