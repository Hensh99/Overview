# Docker Overview

## What is Docker?

- **Virtualization Software:** Docker is a platform for developing, shipping, and running applications inside lightweight containers.
- **Simplifies Development and Deployment:** It makes developing and deploying applications easier by packaging them with all the necessary dependencies, configuration, system tools, and runtime.

## What is a Container?

- **Standardized Unit:** A container is a standardized unit that encapsulates an application along with everything it needs to run.
- **Portable Artifact:** Containers are portable, making them easy to share and distribute.

## Development Process Before Containers

- **Manual Configuration:** Developers had to manually install and configure all services on their local machine's OS.

## Development Process With Containers

- **Isolated Environment:** Each service runs in its own isolated environment.
- **Packaged Services:** Services like PostgreSQL are packaged with all dependencies and configurations.
- **Simplified Commands:** Start services as Docker containers using a single Docker command, with consistent commands across different OS and services.

## Operating System Structure

- OS Application Layer -- OS Kernel -- Hardware

- **Kernel:** The core of every operating system, responsible for interacting between hardware and software components.

## Docker vs. Virtual Machine

### Docker:

- Contains only the **OS Application Layer**.
- Services and applications are installed on top of this layer.

### Virtual Machine:

- Contains both the **OS Kernel** and **OS Application Layer**.

**Note:** Docker images are much smaller than virtual machines.

## Docker Basics

### Commands

- **List all Docker images:**

  ```bash
  docker images
  ```

- **List running containers:**
  ```bash
  docker ps
  ```

## Docker Registries

- **Definition:** A storage and distribution system for Docker images.
- **Docker Hub:** The largest Docker registry, hosting official images for applications like Redis, MongoDB, PostgreSQL, etc.
- The Docker team reviews and publishes all content in the Docker official image repositories.

## Image Versioning

- **Technology Evolves:** Image versions update as technology evolves (e.g., Redis 6.0.x to Redis 6.2.x).
- **Tags:** Docker images are versioned and different versions are identified by tags.

### Commands

- **Pull an image from a registry:**

```bash
 docker pull {name}:{tag}
# Example:
docker pull nginx:1.23
```

- **Pull the latest tag of an official image:**

```bash
docker pull {name}
```

- **Run a Docker image:**

```bash
docker run {name}
```

- **Run a Docker image without blocking the terminal (detached mode):**

```bash
docker run -d {name}
```

- **View Docker logs for a container:**

```bash
docker logs {container}
```

<h3>Note: You don’t need to pull the image before running it; Docker automatically pulls the image if it’s not available locally.</h3>

## Networking: Container Port vs Host Port

- **Isolated Network:** Applications inside containers run in an isolated Docker network.
- **Port Binding:** To expose a container's port to the host (the machine running the container), bind the container port to the host port.

### Common Default Ports

- Redis: 6379
- Nginx: 80
- MySQL: 3306

### Commands

- **Run a Docker container with port binding:**

```bash
docker run -d -p {host_port}:{container_port} {name}:{tag}
# Example:
docker run -d -p 9000:80 nginx:1.23
```

<h3>Note: Only one service can run on a specific port on the host. It’s standard to use the same port on your host as the container is using.</h3>

- **List all containers (running or stopped):**

```bash
docker ps -a
```

- **Start an exited container:**

```bash
docker start {container_id}

```

- **Assign a name to the container:**

```bash
docker run --name web-app -d -p 9000:80 nginx:1.23

```

## Private Docker Registries

- **Docker Hub:** The largest public registry.
- **Private Registries:** You can create private Docker registries (e.g., Amazon ECR) to keep your images private and secure.

## Docker Registry vs Docker Repository

- **Docker Registry:** A service providing storage and a collection of repositories (e.g., Docker Hub).
- **Docker Repository:** A collection of related images with the same name but different versions.

## Dockerfile: Creating Your Own Images

- **Purpose:** To deploy your application as a Docker container.
- **Dockerfile:** A text document containing commands to assemble an image.

## Structure of Dockerfile

- **Base Image:** Dockerfiles start with a parent image or "base image" that your image is based on.

- **WORKDIR:** Sets the working directory for all following commands, similar to using `cd` in a terminal.

```bash
WORKDIR /app
```

- **RUN:** Execute commands in the container, e.g., installing dependencies.

```bash
RUN npm install

```

- **CMD:** Specifies the command to run when the container starts. There can only be one `CMD` instruction in a Dockerfile.

```bash
CMD ["node", "server.js"]
```

## Build and Run Your Docker Image

- **Build Docker Image:**

```bash
docker build -t node-app:1.0 .
```

- **Run as Docker Container:**

```bash
docker run node-app:1.0
```
