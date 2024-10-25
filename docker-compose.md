
# Docker Compose

Docker Compose is a tool that allows you to run multiple containers together. It uses a YAML file to configure and maintain the application's services. With a single command, you can start all services defined in your configuration.



- **Networking**: By default, Docker Compose creates a new network and deploys containers within that network.
- **Mixed Logs**: It consolidates logs from all containers, making it easier to monitor and debug your applications.

## Example

Here’s an example of a `docker-compose.yml` file:

```yaml
version: '3.8'

services:
  mongo:
    image: mongo:latest
    container_name: mongo-db
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongo-data:/data/db

  mongo-express:
    image: mongo-express:latest
    container_name: mongo-express
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD_FILE: /run/secrets/mongo_root_password
      ME_CONFIG_MONGODB_URL: mongodb://admin:password@mongo:27017/
      ME_CONFIG_BASICAUTH_USERNAME: user
      ME_CONFIG_BASICAUTH_PASSWORD: userpass
    depends_on:
      - mongo

volumes:
  mongo-data:

secrets: 
  mongo_root_password:
    file: ./my-secret.txt

```

## Variables/Placeholders in Docker Compose

### 1. Environment Variables

You can use environment variables in your configuration. For example:

```yaml
environment:
  user: ${MONGO_USER}
  passwd: ${MONGO_PASS}
```

### 2. Secrets

You can manage sensitive information, such as passwords, with secrets:

```yaml
secrets:
  my_sect:
    file: ./my-secret.txt
```

## Common Docker Compose Commands

Here are some frequently used Docker Compose commands:

- `docker-compose -f <compose-file> up`: Start and run containers as defined in the compose file.
- `docker-compose -f <compose-file> down`: Remove all containers defined in the compose file.
- `docker-compose -f <compose-file> stop`: Stop running containers.
- `docker-compose -f <compose-file> start`: Start stopped containers.
- `docker compose --project-name <name> -f <compose-file> up -d`: Run the containers in detached mode with a specified project name.

## How Docker Private Registry Works with Docker Compose

After running `docker login`, Docker saves your authentication token in `config.json`. Docker Compose utilizes this token to pull images from the private registry automatically.
