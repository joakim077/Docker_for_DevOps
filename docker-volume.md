
# Docker Volumes

Containers are ephemeral, meaning they lose all their data when destroyed. To persist data beyond the lifecycle of a container, Docker provides volumes. A volume is a storage unit that exists independently of containers, retaining data even if the container is removed.

By creating Docker volumes and mapping or sharing them with containers, you ensure the data outlives the container's lifecycle.

## Steps to Use Docker Volumes

### 1. Create a Docker Volume

You can declare a volume in a container in two ways:

- **From a Dockerfile**:
    ```dockerfile
    FROM ubuntu
    VOLUME ["/myVolume1"]
    ```

- **From the CLI**:
    ```bash
    docker run -itd --name <container_name> -v /<dir> <image> /bin/bash
    ```

### 2. Map a Volume

- **Container to Container**:
    ```bash
    docker run -it --name <destination_container> --privileged=true --volumes-from <source_container>
    ```

- **Host to Container**:
    ```bash
    docker run -it --name <container_name> -v /host_directory:/container_directory --privileged=true <image> /bin/bash
    ```

## Useful Docker Volume Commands

- List all volumes:
    ```bash
    docker volume ls
    ```

- Create a new volume:
    ```bash
    docker volume create <volume_name>
    ```

- Remove a specific volume:
    ```bash
    docker volume rm <volume_name>
    ```

- Remove all unused volumes:
    ```bash
    docker volume prune
    ```

- Inspect a specific volume:
    ```bash
    docker volume inspect <volume_name>
    ```

- Inspect a container's volume usage:
    ```bash
    docker container inspect <container_name>
    ```

## Benefits of Docker Volumes

- **Decouples Storage from Containers**: Volumes exist independently of the containers, so data persists even when containers are deleted.
- **Share Volumes Across Containers**: Multiple containers can access and use the same volume.
- **Data Persistence**: Since volumes are not tied to the lifecycle of a container, deleting a container does not delete its associated volume unless explicitly removed.

Docker volumes provide a powerful way to manage data persistence and sharing across containers and hosts.
