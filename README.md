# Docker Overview

## What is Docker?
Docker is an open-source platform designed to automate the deployment, scaling, and management of applications using containers.

### Containers
Docker containers are lightweight, portable, and isolated environments that package an application along with its dependencies, libraries, and configurations.

### Images
Containers are created from Docker images, which are templates containing everything needed to run an application.

### Dockerfile
A Dockerfile is a text file with instructions to automate the building of a Docker image, specifying the base image, dependencies, and configuration for running an application in a container.

### Docker Hub
Docker Hub is a public registry where you can find, share, and store Docker images. It acts as the central hub for images.

---

## Docker Architecture

At the core of Docker is the **Docker Engine**, responsible for creating, running, and managing containers. It operates with two main components:

- **Client**: The interface where users issue commands, such as building images or running containers. These commands are sent to the Docker daemon.
- **Daemon**: The background service (also called `dockerd`) that handles container lifecycle management, including building, running, stopping, and removing containers based on commands from the client. Includes containerd as a core component.

---

## Docker Workflow

1. **Write Dockerfile**: Define your app and its dependencies.
2. **Build Image**: Create an image using `docker build`.
3. **Run Container**: Start your application inside a container using `docker run`.
4. **Push to Registry**: Share the image by pushing it to Docker Hub or a private registry.
5. **Pull Image**: On other systems or environments, pull the image using `docker pull`.
6. **Run Anywhere**: Deploy the containerized app consistently across different environments.

---

## Common Docker Commands

- `docker images`: List images in the Docker engine.
- `docker search <image>`: Search for images in Docker Hub.
- `docker pull <image>`: Pull an image from Docker Hub.
- `docker run -it <image> /bin/bash`: Run a container interactively (-i -> interactive, -t -> terminal).
- `docker run -it --name <containername> <image> /bin/bash`: Run a container with a specific name.
- `docker start <containername>`: Start a stopped container.
- `docker attach <containername>`: Attach to a running container (use `Ctrl + P + Ctrl + Q` to detach).
- `docker exec <containername> <command>`: Run a command inside a running container.
- `docker ps`: List running containers (`-a` for all containers).
- `docker stop <containername>`: Stop a running container.
- `docker kill <containername>`: Sends a SIGKILL signal to a running container, terminating it immediately
- `docker rm <containername>`: Remove a stopped container.
- `docker rmi <image>`: Remove an image.

---

## Creating Docker Images

### 1. From a Running Container
- Use `docker diff <containername>` to see changes made in the container.
- Commit those changes with `docker commit <containername> <imagename>`.

### 2. From a Dockerfile
`docker build -t <tagname> .`

Dockerfile components:
- `FROM`: Base image for your container.
- `MAINTAINER`: Maintainer information.
- `WORKDIR`: Set working directory inside the container.
- `COPY`: Copy files from the host into the container.
- `ADD`: Add files, directories, or remote files into the container.
- `ENV`: Set environment variables.
- `RUN`: Run commands inside the image at build time.
- `EXPOSE`: Expose a port to enable access to the container.
- `ENTRYPOINT`: Configure a container to run as an executable.
- `CMD`: Provide default commands for a container when it starts.

---

This guide offers a high-level overview of Docker, its architecture, workflow, and commonly used commands.
