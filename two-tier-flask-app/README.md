# Flask App with MySQL Docker Setup

This guide will help you set up and run a simple Flask application that interacts with a MySQL database using Docker. The app allows users to submit messages, which are stored in the database and displayed on the frontend.

## Prerequisites

Ensure you have the following installed on your system:

- **Docker** (for containerization)
- **Git** (optional, for cloning the repository)

### Start the Docker Containers
Use Docker Compose to build and start the containers:
```bash
docker-compose up --build
```
### Access the Application
Once the containers are up, you can access the app from your browser: http://localhost:5000

To stop and remove the Docker containers, press Ctrl + C in the terminal where the containers are running, or use:

```bash
docker-compose down
```

### Running the Application Without Docker Compose
If you prefer to run the Flask app and MySQL container without Docker Compose, follow these steps:

1. Build the Flask App Docker Image
    ```bash
    docker build -t flaskapp .
    ```
2. Create a Docker Network
Ensure both containers are on the same Docker network for communication:
    ```bash
    docker network create twotier
    ```
3. Run the MySQL Container
Start the MySQL container and attach it to the twotier network:
    ```bash
    docker run -d \
        --name mysql \
        -v mysql-data:/var/lib/mysql \
        --network=twotier \
        -e MYSQL_DATABASE=mydb \
        -e MYSQL_ROOT_PASSWORD=admin \
        -p 3306:3306 \
        mysql:5.7
    ```
4. Run the Flask App Container
Start the Flask app container and attach it to the same network:
    ```bash
    docker run -d \
        --name flaskapp \
        --network=twotier \
        -e MYSQL_HOST=mysql \
        -e MYSQL_USER=root \
        -e MYSQL_PASSWORD=admin \
        -e MYSQL_DB=mydb \
        -p 5000:5000 \
        flaskapp:latest
    ```

