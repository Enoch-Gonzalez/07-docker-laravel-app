# Laravel Dockerized Development Environment

This project is a Dockerized development environment for a Laravel PHP application. This project demonstrates how to set up a local development environment for a Laravel PHP application using Docker.

## Project Structure

The project consists of several components and configuration files. Here's an overview of the project structure:

### Dockerfiles

- **composer.dockerfile**: Dockerfile for setting up a Composer container.
- **nginx.dockerfile**: Dockerfile for configuring an Nginx container.
- **php.dockerfile**: Dockerfile for configuring a PHP-FPM container.

### Env

- **mysql.env**: Environment variables for MySQL database configuration.

### Nginx

- **nginx.conf**: Nginx server configuration for routing requests to the Laravel application.

### Src (Development Phase)

- This directory is automatically populated with your Laravel application source code thanks to the bind mounts defined in the `docker-compose.yaml` file. During the development phase, any modifications you make to your application code will be immediately visible in the running containers.

- The bind mounts ensure that the Laravel application source code is synchronized with the containers, allowing you to see live changes without needing manual intervention.

### docker-compose.yaml

- Configuration file for Docker Compose that defines the services and containers for your development environment. This file is configured for a development phase of a project.

## Prerequisites

Before you get started, ensure you have the following prerequisites installed on your system:

- Docker
- Docker Compose (separate installation for Linux users)

## Getting Started

Follow these steps to set up your Laravel development environment using Docker:

1. Clone this repository to your local machine.

2. Configure your Laravel application to use the MySQL database. You can do this by modifying your Laravel application's `.env` file with the database credentials specified in the `mysql.env` file. (Data will not persist since there are no volumes).

3. Create the laravel project:

    ```docker    
    docker-compose run --rm composer create-project --prefer-dist laravel/laravel:^8.0 .
     ```

4. Open src/.env in your editor and change the configuration lines for the database connection as follows:

- DB_DATABASE=homestead
- DB_USERNAME=homestead
- DB_PASSWORD=secret

5. Build the Docker containers using `--build` to make sure you are getting the latest image and start the development environment using the following command:

    ```docker
    docker-compose up mysql server php
     ```

6. Once the containers are up and running, you can access your Laravel application in your web browser at http://localhost:8000.

7. You can run Artisan commands, Composer, and other utilities in the running containers by using docker-compose run. For example, to run Laravel's Artisan migrate command:

    ```docker
    docker-compose run artisan migrate
     ```

8. When you are finished working, stop and remove the containers with the following command:

    ```docker
    docker-compose down
     ```

## Customization

You can customize this development environment by modifying the Dockerfiles, Nginx configuration, and other files to match your specific project requirements. For example if the code is changed in the /src/resources/views/welcome.blade.php the changes will be reflected in the app.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is open-source and available under the MIT License. You are free to use and modify it for your own projects.
