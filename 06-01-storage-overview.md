# Storage Overview

In this lesson, we will look a how Docker handles storage for persistent and non-persistent data.

## Docker Storage 101
Categories of data storage:
- Non-persistent
  - Local storage
  - Data that is ephemeral
  - Every container has it
  - Tied to the lifecycle of the container
- Persistent
  - Volumes
     - Volumes are decoupled from containers

## Non-persistent Data
Non-persistent data:
- By default all container use local storage
- Storage locations:
  - Linux: /var/lib/docker/[STORAGE-DRIVER]/
  - Windows: C:\ProgramData\Docker\windowsfilter\
- Storage Drivers:
  - RHEL uses overlay2.
  - Ubuntu uses overlay2 or aufs.
  - SUSE uses btrfs.
  - Windows uses its own.

## Persistent Data Using Volumes
Volumes:
- Use a volume for persistent data:
  - Create the volume first, then create your container.
- Mounted to a directory in the container
- Data is written to the volume
- Deleting a container does not delete the volume
- First-class citizens: volume are their own object, they have their own APIs as well as their own subcommand.
- Uses the local driver by default
- Third party drivers:
  - Block storage: Good for high performance or small block random access workloads (AWS EBS, Openstack Cinder)
  - File storage: use protocol like NFS, SMB, Good for high performance workloads like block storage (Netapps FAS, Azure file storage, Amazon EFS)
  - Object storage: Large data blobs that don't change all that often(AWS S3, Ceph, MinIO, Openstack Swift)
- Storage locations:
  - Linux: /var/lib/docker/volumes/
  - Windows: C:\ProgramData\Docker\volumes