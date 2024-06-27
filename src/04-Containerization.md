![banner](images/banner_1.jpg)

# Containerizing With Docker

Docker containers are `self-contained` units that include everything an application needs to run, from its code to its `libraries` and dependencies. This makes them highly portable and allows them to run consistently on any system with Docker installed, regardless of the underlying operating system. Simply put, it solves the *"It worked on my machine"* problem.

![docker_meme](images/docker_meme.jpg)

Here's an example of a simple Dockerfile that runs a Nginx web server

```yaml
# Use the official nginx image as the base
FROM nginx:latest

# Copy the contents of the current directory to /usr/share/nginx/html in the container
COPY . /usr/share/nginx/html

# Expose port 80 (the default web server port)
EXPOSE 80

# Run the nginx command
CMD ["nginx", "-g", "daemon off;"]

```
# Docker Concepts

![docker architecture](images/docker_architecture.jpg)

| Name          | Description                           |
|---------------|---------------------------------------|
| Container     | A box filled with dependencies        |
| Client        | Where we run docker commands          |
| Host          | Where containers live                 |
| Daemon        | Who manages docker operations         |
| Registry      | Where images live                     |
| Images        | A container blueprint                 |
| Dockerfile    | Who creates images                    |
| Objects       | Instances of things like images       |
| Storage       | A place to keep files                 |

![dockerfile workflow](images/dockerfile_workflow.jpg)

# Docker Engine vs Docker Desktop

Docker Engine is a lower-level tool, geared towards system administrators. On the other hand, Docker Desktop provides a user-friendly interface and additional tools for developers.

# Installing Docker Engine

The easiest way to install Docker is with a convenience script they provide.

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

# Pulling a Docker Image

By pulling an image from a public repository like Docker Hub, you can quickly deploy a pre-built application without having to manually install all the dependencies yourself. Let's pull the `hello-world` image.

```bash
sudo docker pull hello-world
```
# Checking the images

```bash
sudo docker images

```
# Running the image

```bash
sudo docker run hello-world
```

#   

# Install Docker Compose

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
