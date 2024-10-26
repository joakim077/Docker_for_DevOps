# MongoDB & Mongo Express Project

This project demonstrates how to run a MongoDB database and Mongo Express (a web-based MongoDB admin interface) using Docker Compose.

## Setup

1. Ensure that Docker and Docker Compose are installed on your system.
2. Navigate to the project directory.
3. Run the following command to start the services:
   ```bash
   docker-compose up
   ```
4. Access Mongo Express at `http://localhost:8081` to interact with your MongoDB instance.

## docker-compose.yaml

The `docker-compose.yaml` file sets up two services:
- **MongoDB**: A popular NoSQL database.
- **Mongo Express**: A web-based interface to manage MongoDB.



## Notes

- MongoDB is accessible on port `27017`.
- Mongo Express is accessible on port `8081`.
- The MongoDB username and password are set in the environment variables as `admin` and `root123`. These can be changed for security.
