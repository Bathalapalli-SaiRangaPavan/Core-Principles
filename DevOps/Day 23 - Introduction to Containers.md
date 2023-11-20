# Day 23 - Introduction to Containers

Note - Understand virtual machines before diving into containers.
## Virtual Machines (VMs)
- VMs are an advancement to physical servers.
- Hypervisor uses virtualization to create multiple virtual machines on a physical server.
- Each VM has its own operating system, providing logical separation for running applications.
- VMs solved the problem of underutilizing resources on physical servers.

## Why Move Towards Containers?
- Containers address resource wastage in VMs.
- VMs may not utilize resources efficiently, leading to wastage and increased costs.
- Containers aim to optimize resource usage and reduce wastage.
- Unlike VMs, containers are lightweight and share resources from the host OS.

## Architecture of Containers
### Two Models for Container Creation
#### Model 1:
- Containers created on top of physical servers.
- Containerization platform installed on the server to create containers.

#### Model 2:
- Containers created on top of virtual machines (VMs).
- Can be on cloud provider's VMs or on-premises physical servers.
- More organizations prefer Model 2 for reduced maintenance overhead.

### Characteristics of Containers
- Containers are lightweight, as they do not have a complete operating system.
- Containers share resources from the base operating system or the VM/physical server.
- Docker containers, for example, consist of application, application libraries, and minimal OS/system dependencies.
- Container images are significantly smaller than VM snapshots, making them easy to ship.

## Why Docker is Popular?
- Docker introduced a user-friendly interface for containerization.
- Docker simplifies container creation using Dockerfiles and engine commands.
- Docker's popularity is attributed to its contribution to improving containerization concepts.

## Lifecycle of Containers
1. **Write a Dockerfile:** Defines the contents and configuration of a container.
2. **Build Image:** Use the build command to create a Docker image from the Dockerfile.
3. **Create Container:** Use the run command to create a container from the Docker image.

## Challenges with Docker
- Docker Engine is a single point of failure; if it goes down, all containers stop.
- Docker images have multiple layers, leading to storage challenges.

## Buildah as an Alternative
- **Buildah:** A tool to build container images with a focus on addressing Docker's challenges.
- Solves the layering problem and provides simplicity.
- Works well with Scopio and Podman.
- Buildah relies on command-based scripting for image creation.
