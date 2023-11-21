## Day 24: Basics to Best Practices

### Goals
- Why containers are lightweight in nature?
- Files and folders in container base images
- Files and folders containers use from the host operating system
- What is Docker?
- Architecture of Docker
- Docker life cycle
- Docker registry
- GitHub vs Dockerhub
- Create a Docker account
- Install Docker
- Write your first Dockerfile
- Create an image
- Execute the Docker Image
- Push the image to DockerHub
- Pull Docker image from DockerHub 

### Why Containers are Lightweight in Nature?
Containers are lightweight because they don't include a full operating system. They consist of the application, its dependencies, and essential system dependencies. Unlike virtual machines, containers share the host OS kernel, utilizing critical resources only when running. This efficiency allows running multiple containers on a single virtual machine without incurring the same overhead as VMs.

### Files and Folders in Container Base Images
1. **/bin:** Binary executable files (e.g., ls, cp).
2. **/sbin:** System binary executable files (e.g., init, shutdown).
3. **/etc:** Configuration files for various system services.
4. **/lib:** Library files used by binary executables.
5. **/usr:** User-related files and utilities.
6. **/var:** Variable data, like log files and temporary files.
7. **/root:** Home directory of the root user.

These files and folders create logical isolation between containers and are part of the container base image.

### Files and Folders Containers Use from Host OS
1. **Host File System:** Containers can access the host file system using bind mounts.
2. **Networking Stack:** Host's networking stack provides connectivity to the container.
3. **System Calls:** Containers use system calls handled by the host's kernel to access resources.
4. **Namespaces:** Linux namespaces create isolated environments for processes.
5. **Control Groups (cgroups):** Used to limit and control container resources (CPU, memory, I/O).

Containers leverage these aspects from the host OS for functionality.

### What is Docker?
Docker is a containerization platform that allows you to package and distribute applications and their dependencies in a standardized unit called a container. It simplifies application deployment, provides consistency across different environments, and enhances scalability.

### Architecture of Docker
- **Docker Client (CLI):** User interacts with Docker using commands.
- **Docker Daemon:** Listens for Docker CLI commands and manages containers and images.
- **Docker Images:** Snapshots of file systems and configurations.
- **Docker Containers:** Running instances of Docker images.
- **Docker Registry:** Centralized repository for storing and sharing Docker images.

The Docker daemon is the core component, executing commands received from the Docker CLI.

### Docker Life Cycle
1. **Write Dockerfile:** Contains instructions to build a Docker image.
2. **Build Image:** Docker daemon builds an image based on the Dockerfile.
3. **Create Container:** Run the Docker image to create a container.
4. **Share or Push:** Push the image to a registry for sharing.

Docker simplifies application development, testing, and deployment by encapsulating dependencies and configurations.

### Docker Registry
A Docker registry is a repository for storing and sharing Docker images. DockerHub is a popular public registry, while private registries offer more control over image distribution within organizations.

### GitHub vs Dockerhub
- **GitHub:** Version control platform for source code.
- **DockerHub:** Version control platform for Docker images.

GitHub stores source code, while DockerHub stores Docker images for sharing and distribution.

### Install Docker
1. Create an EC2 instance (e.g., Ubuntu).
2. Install Docker: `sudo apt update` -> `sudo apt install docker.io -y`.
3. Check status: `sudo systemctl status docker`.
4. Add user to Docker group: `sudo usermod -aG docker ubuntu`.

### Write Your First Dockerfile
1. Clone a repository: `git clone https://github.com/iam-veeramalla/Docker-Zero-to-Hero.git`.
2. Navigate to the Dockerfile directory: `cd Docker-Zero-to-Hero/examples/first-docker-file`.
3. Copy `app.py` to the current directory: `cp ../app.py .`.
4. Create a Dockerfile: `vi Dockerfile`.
   ```Dockerfile
   FROM ubuntu:latest
   WORKDIR /app
   COPY . /app
   RUN apt-get update && apt-get install -y python3 python3-pip
   ENV NAME World
   CMD ["python3", "app.py"]

### Build and Push Docker Image

To build the Docker image, run the following command in the terminal:

```
docker build -t username/repo:tag .
```
Replace username/repo:tag with your desired image name and tag.

### Execute the Docker Image

To see the application running, execute the following command in the terminal:

```
docker run -it abhishekf5/my-first-docker-image:latest
```
### Push Image to DockerHub
Login to DockerHub using the following command:
```
docker login
```
Enter your DockerHub username and password when prompted.
Push the Docker image to DockerHub with the following command:
```
docker push username/repo:tag
```
Replace username/repo:tag with the same image name and tag used during the build.

### Pull Docker Image from DockerHub

To verify and pull the Docker image, run the following command in the terminal:
```
docker pull abhishekf5/my-first-docker-image:latest
```
### Conclusion
Understanding Docker basics and best practices is crucial for efficient application development, testing, and deployment. Containers offer lightweight, consistent environments, and Docker simplifies the containerization process, making it a powerful tool for developers and DevOps teams.
