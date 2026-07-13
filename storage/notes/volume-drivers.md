# Volume Drivers

## Difference between storage drivers and volume drivers
- Storage drivers manage image and container layers.
- Volume drivers manage persistent data volumes.

## Docker volumes
If you want data to survive container removal, use a volume.

Example:
```bash
docker run -v data_volume:/var/lib/mysql mysql
```

Docker creates a volume named `data_volume` if it does not already exist.

The volume is stored under a Docker-managed path such as:
```bash
/var/lib/docker/volumes/data_volume/_data
```

## Cloud and plugin-based volume drivers
Volume drivers can integrate with external storage systems such as:
- RexRay for AWS EBS
- Portworx
- NFS-based plugins

## Exam points
- Volumes are used for persistence.
- Volume drivers help connect Docker or Kubernetes to external storage backends.
- This is different from the basic filesystem layer managed by storage drivers.
