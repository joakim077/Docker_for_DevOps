# Docker Networking

## Key Networking Concepts

- **Network Interface**: Acts as the connection point between a device and a network.
  
- **Gateway**: A gateway connects different networks and translates data between networks that may use different protocols or addressing schemes.

- **Network Adapter (NIC)**: Refers to the physical hardware (a network card or built-in chip) that allows a device to connect to a network.

## Docker Network Types

### 1. Default Bridge Network

- The default bridge network provides isolation between your network and containers.
- By default, when you deploy a container, it is attached to this bridge network.
- You can inspect the `docker0` virtual network interface:
    ```bash
    ip addr show
    ```

- **docker0 Interface**:
    - Containers can communicate with the internet through the `docker0` gateway.
    - The bridge network has:
        - **DHCP**: Automatically assigns IP addresses to containers.
        - **DNS**: Copies the host's `/etc/resolv.conf` to the container.

### 2. Custom Bridge Network

- Custom bridge networks offer greater control over container isolation, security, performance, and communication.
- **Service discovery**: Containers can find and communicate with each other by name when connected to the same custom network.

- Commands to create and run containers on a custom network:
    ```bash
    docker network create <network_name>
    docker run -p 80:80 --network <network_name> <image_name>
    ```

### 3. Host Network

- The host network mode runs a container as if it were part of the host's network stack, eliminating network isolation.
- No need to expose ports manually because the container shares the host’s IP and ports.
- Example:
    ```bash
    docker run -itd --rm --network host --name web nginx
    ```

## Useful Docker Networking Commands

- **Display network interfaces**:
    ```bash
    ip addr show
    ip route
    ```

- **Bridge interface details**:
    ```bash
    bridge link
    ```

- **Create a new network**:
    ```bash
    docker network create <network_name>
    ```

- **List available networks**:
    ```bash
    docker network ls
    ```

- **Inspect detailed information about a network**:
    ```bash
    docker inspect <network_name>
    ```

- **Connect a container to a network**:
    ```bash
    docker network connect <network_name> <container_name>
    ```

- **Disconnect a container from a network**:
    ```bash
    docker network disconnect <network_name> <container_name>
    ```

- **Remove all unused networks**:
    ```bash
    docker network prune
    ```

- **Remove a specific network**:
    ```bash
    docker network rm <network_name>
    ```

## Other Useful Docker Commands

- **Inspect a container**:
    ```bash
    docker inspect <container_name>
    ```

- **Display container port mappings**:
    ```bash
    docker port <container_name>
    ```

- **Display running processes in a container**:
    ```bash
    docker top <container_name>
    ```

- **Monitor container resource usage**:
    ```bash
    docker stats
    ```

- **Save a Docker image to a file**:
    ```bash
    docker save <image_name> > <file_name>.tar
    ```

- **Load a Docker image from a file**:
    ```bash
    docker load < <file_name>.tar
    ```

Docker's networking capabilities provide flexible ways to isolate, connect, and manage communication between containers and with the host system.


