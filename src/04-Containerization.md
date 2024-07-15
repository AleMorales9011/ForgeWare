![banner](images/banner_1.jpg)

# Containerizing With Docker Engine

Docker containers are `self-contained` units that include everything an application needs to run, from its code to its `libraries` and dependencies.

Simply put, it solves the *"It worked on my machine"* problem.

![docker_meme](images/docker_meme.jpg)

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

```ruby
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

# Pulling a Docker Image

By pulling an image from a public repository like Docker Hub, you can quickly deploy a pre-built application without having to manually install all the dependencies yourself. Let's pull the `hello-world` image.

```ruby
sudo docker pull hello-world
```

# Checking the images

```ruby
sudo docker images

```
![sudo-docker-images](images/sudo-docker-images.jpg)

# Running the image

```ruby
sudo docker run hello-world
```
![sudo-run-hello-world](images/sudo-docker-run-hello-world.jpg)

# Running an Interactive Image in the Background

In most cases, you'll likely use the `-d` or `-it` flags along with the `run` command.

1. Use `-d` for background processes or services.
2. Use `-it` to start a container in the foreground and interact with it like a regular terminal session.

# Docker --Help
Use `sudo docker --help` to see all commands and `sudo docker <command> --help` to see all available flags(options) for the command. 

![sudo-docker-help](images/docker-help.jpg)

# Usefull Docker Commands

| Name                                                 | Description                              |
|------------------------------------------------------|------------------------------------------|
| docker rm `id`                                       | Removes containers                       |
| docker rmi `name`                                    | Removes images                           |
| docker ps                                            | List containers                          |
| docker stop `id`                                     | Stop a running container                 |
| docker run `-dti --name container image`             | Name a container                         |
| docker exec `-ti Ubuntu /bin/bash`                   | Executes bash inside Ubuntu              |
| docker exec `Ubuntu mkdir /destiny`                  | Creates a `destiny` inside the container |
| docker `cp file container:/destiny`                  | Copy to container from local machine     | 
| docker `cp container:/originfolder/file newfilename` | Copy to local machine from container     | 
| docker pull debian:9                                 | Pulls specific Debian container version  | 

# Installing a MYSQL container

Running a MYSQL database in a container prevents conflicts with other software or system-wide configurations.

```ruby
docker pull mysql
```

# Running a MySQL container

```ruby
docker run -e MYSQL_ROOT_PASWORD=password --container name -d -p 3306:3306 imagename
```
1. `-e` Sets environmental variables.
2. `-d` Executes the database in the background.
3. `-p` Opens a port to communicate with the database. 



# Install Docker Compose

Before executing the yaml file it's important to install docker compose. This task is achieved by coding the following command into the terminal.

```ruby
apt install docker-compose
```

# Create the YML file

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

# Executing the script

Finally, we must execute the script so our infrastructure( in this case our Apache web server) will be created. We can do that by typing the following command into the console.

```ruby
docker-compose up -d
```

# Conclusion

Docker Compose manages adding or removing service instances with ease. Finally, version control of the YAML configuration file simplified version management for all their services.
In short, Docker Compose helped Acme Corp. achieve faster development cycles, smoother deployments, and better scalability for their application.
