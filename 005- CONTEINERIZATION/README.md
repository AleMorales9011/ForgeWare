## Conteinarization
Acme Corp was struggling with its complex application. Developers battled with inconsistent environments, leading to bugs. Deployments were slow and cumbersome, requiring manual intervention for each service. Docker Compose came to the rescue! With a single YAML file, Docker Compose ensured a uniform development environment for everyone, eliminating bugs caused by environment mismatches. Deploying the entire application became a one-click operation, streamlining the process significantly.

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
