# Open Container Initiative (OCI)

The Open Container Initiative (OCI) is an open governance project under the Linux Foundation that defines industry standards for container formats and runtimes.

Its goal is to make container technologies interoperable across tools such as Docker, Kubernetes, containerd, and other runtimes.

## The three main OCI specifications

### 1) Image Specification (image-spec)
This is the standard that defines the structure, format, and metadata of container images.

It answers the exam-style question:
- The correct answer is: `image-spec`
- It defines how an image is packaged and described so that different tools can work with it consistently.

An OCI image typically includes:
- an image manifest
- an image configuration file
- one or more filesystem layers

This is the spec that ensures container images can be built, stored, and run in a portable way.

Example tools and technologies that implement or rely on this spec:
- Docker: builds and runs OCI-compliant images
- containerd: pulls and manages OCI images
- Kubernetes: runs containers from OCI images
- Buildah and Podman: build and manage OCI images

### 2) Runtime Specification (runtime-spec)
This spec defines how a container runtime should execute a container from a filesystem bundle.

It focuses on:
- container lifecycle
- process execution
- filesystem and runtime behavior

In simple terms, `runtime-spec` is about how containers are run, not how images are structured.

Example tools and technologies that implement this spec:
- runc: a widely used OCI runtime
- containerd: uses OCI runtime concepts for container execution
- CRI-O: implements container runtime behavior for Kubernetes

### 3) Distribution Specification (distribution-spec)
This spec defines how container images should be distributed and fetched from registries.

It is about:
- image pull/push workflows
- registry APIs
- transport and distribution of content

It helps standardize how images move between registries and clients.

Example tools and technologies that use or support this spec:
- Docker Hub: a public container registry
- Harbor: an enterprise container registry
- Azure Container Registry: a managed OCI image registry
- Google Artifact Registry: supports container image distribution

## KCNA exam takeaway
If a question asks:
- “Which OCI spec defines the structure, format, and metadata of container images?”

The answer is:
- `image-spec`

## Quick memory trick
- `image-spec` = image format and metadata
- `runtime-spec` = how the container runs
- `distribution-spec` = how images are distributed

## Why OCI matters in Kubernetes
Kubernetes relies on container images as the unit of deployment. OCI standards help ensure that images built by one tool can be consumed by another in a consistent and portable way.




