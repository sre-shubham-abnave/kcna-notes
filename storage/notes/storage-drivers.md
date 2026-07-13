

# Storage Drivers (Docker Basics)

## What are storage drivers?
Docker uses storage drivers to manage how image layers and container data are stored on disk.

## Docker storage layout
Docker stores container data under the directory:
- `/var/lib/docker`

This folder contains data for images, containers, and volumes.

## Layered image architecture
Each instruction in a Dockerfile creates a new layer.

Example layers:
- Base Ubuntu layer
- Installed packages
- Application code
- Entrypoint changes

These image layers are read-only.

## Copy-on-write
When a container changes a file from the image, Docker does not modify the original file directly. Instead, it creates a copy of that file in the container's writable layer.

This is called copy-on-write.

## Container writable layer
When a container runs, it has a writable layer for:
- logs
- temporary files
- application changes

If the container is removed, this writable layer is also removed.

## Mounting in Docker
- Volume mount: mounts a Docker-managed volume.
- Bind mount: mounts a directory from the host machine.

Example:
```bash
docker run --mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql
```

## Common storage drivers
Docker has used different storage drivers such as:
- AUFS
- ZFS
- BTRFS
- Device Mapper
- Overlay
- Overlay2

## Exam points
- Storage drivers are about image/container storage management.
- They are different from Kubernetes persistent volumes.


