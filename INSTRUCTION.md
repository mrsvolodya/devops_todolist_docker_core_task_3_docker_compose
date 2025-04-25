# Docker Compose Instructions for Django-Todolist

This document provides instructions on how to run and manage the Django-Todolist application using Docker Compose.

## Prerequisites

- Docker installed on your system
- Docker Compose installed on your system

## Running the Application

1. **Build and Start Containers**

   ```bash
   docker-compose up --build
   ```

   This command will:

   - Build the Docker images for both the Python application and MySQL database
   - Create a persistent volume for MySQL data
   - Start both containers
   - Run database migrations
   - Start the Django development server

2. **Access the Application**
   - The application will be available at: http://localhost:8080
   - The API will be available at: http://localhost:8080/api/
   - MySQL database will be accessible on port 3306

## Managing Containers

1. **Stop Containers**

   ```bash
   docker-compose down
   ```

   This will stop and remove the containers, but preserve the MySQL data volume.

2. **Stop Containers and Remove Volumes**

   ```bash
   docker-compose down -v
   ```

   This will stop the containers and remove all volumes, including the MySQL data.

3. **View Logs**

   ```bash
   docker-compose logs -f
   ```

   This will show the logs from all containers in real-time.

4. **View Specific Container Logs**
   ```bash
   docker-compose logs -f pythoapp  # For Python application logs
   docker-compose logs -f mysql     # For MySQL logs
   ```

## Troubleshooting

1. **If containers fail to start**

   - Check if port 8080 is available on your system
   - Check if port 3306 is available on your system
   - Run `docker-compose down -v` and try again

2. **If database connection fails**

   - Ensure MySQL container is running: `docker-compose ps`
   - Check MySQL logs: `docker-compose logs mysql`

3. **To rebuild from scratch**
   ```bash
   docker-compose down -v
   docker-compose up --build
   ```

## Environment Variables

The application uses the following environment variables:

- MySQL:
  - MYSQL_ROOT_PASSWORD: 1234
  - MYSQL_DATABASE: app_db
  - MYSQL_USER: app_user
  - MYSQL_PASSWORD: 1234

## Notes

- The MySQL data is persisted in a Docker volume named `db-data`
- The application uses a bridge network `db-data-net` for container communication
- Database migrations are automatically run when the container starts
