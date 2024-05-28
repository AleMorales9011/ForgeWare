# Containerization

Containerization is a way to package an application with everything it needs to run (code, libraries, settings) into a self-contained unit called a container.

## Abstract

Jane's team overcame complex app issues with Docker Compose. It ensured consistent environments, eliminated bugs, and streamlined deployments with a single-click.

## Table of Contents

- Install Docker Compose
- Create the YML file
- Executing the script
- Conclusion

### 1. Install Docker Compose

Before executing the yaml file it's important to install docker compose. This task is simply achieved by coding the following command into the terminal.

```ruby
apt install docker-compose
```

### 2. Create the YML file

After docker-compose is installed we must create the yaml file that will contain the infrastructure we desire to create. The script below shows an example of an Apache web server container deployment.

```ruby
version: '3.9'
services:
  apache:
    image: httpd:latest
    container_name: my-apache-app
    ports:
    - '8081:80'
    volumes:
    - ./website:/usr/local/apache2/htdocs
```

### 3. Executing the script

Finally, we must execute the script so our infrastructure( in this case our Apache web server) will be created. We can do that by typing the following command into the console.

```ruby
docker-compose up -d
```

## Conclusion

Docker Compose manages adding or removing service instances with ease. Finally, version control of the YAML configuration file simplified version management for all their services.
In short, Docker Compose helped Acme Corp. achieve faster development cycles, smoother deployments, and better scalability for their application.
