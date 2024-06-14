![Forgeware](images/Forgeware_banner_final.png)
# Introduction

20 minutes

Software Engineering is a complicated subject. It's hard to break through the `myriad of technologies`, frameworks, good practices, and programming languages. Forgeware exists to demystify Software Engineering in a hands-on way. We try to demonstrate concepts in real-life scenarios and show the code behind those `real-life applications` so you get a sense of what you are dealing with. Please notice the scripts we provide are not meant to be used in any production environment. 

# Automating the creation of users, directories, permissions, and groups with Bash

This script will automate the creation of new developer accounts on the system, assign them directories and permissions based on their role, and add them to relevant development groups. This eliminates manual setup and ensures consistency.
`BEGINNER` `BASH` `LINUX`

```ruby
# Creating directories
sudo mkdir /public  # sudo execute the command with superuser privileges
sudo mkdir /frontend     # mkdir is the command for creating a directory
sudo mkdir /backend
sudo mkdir /ops

# Creating groups
sudo groupadd GRP_FRONTEND  # groupadd creates a new group
sudo groupadd GRP_BACKEND
sudo groupadd GRP_OPS
```

# Implementing a version control system with Git/Github
We will use Git for version control and Github for a central repository. Developers will have access to the latest codebase and can track changes efficiently.
`BEGINNER` `GIT` `GITHUB`
```ruby
git clone <URL>
git add <filename> # to stage specific files for commit.
git commit -m "Meaningful commit message" # to create a snapshot of their changes with a descriptive message
git branch -M main
git remote add origin <repo URL> # This command configures a remote repository.
git push origin <branch_name>
```


# Deploying infrastructure with Terraform
Terraform will automate infrastructure provisionings, such as servers, databases, and storage on a chosen cloud platform. This ensures consistent and repeatable infrastructure deployment.
`INTERMEDIATE` `TERRAFORM` `CLOUD COMPUTING`
```ruby
# Create a Resource Group for desktop 
resource "azurerm_resource_group" "rg-desktop-bknd-001" {  # Define components of your infrastructure
  location = "westeurope"
  name     = "rg-desktop-bknd-001"
  tags     = var.desktop_tags
}

# Create a Resource Group for mobile 
resource "azurerm_resource_group" "rg-mobile-bknd-001" {
  location = "westeurope"
  name     = "rg-mobile-bknd-001"
  tags     = var.mobile_tags
}
```
# Creation of CI/CD pipeline with Azure DevOps

Azure DevOps will be used to create a continuous integration and continuous delivery (CI/CD) pipeline. Upon code commit, the pipeline will automatically build, test, and deploy the application to a staging environment.
`INTERMEDIATE` `AZURE DEVOPS` `DEVOPS`
```ruby
- task: TerraformTaskV4@4 # Executes Terraform commands.
  inputs: # Defines the input parameters for the task
    provider: 'azurerm' # Tells Terraform to use the Azure Resource Manager provider.
    command: 'init' # Specifies the Terraform command to be executed. 
    backendServiceArm: 'bknd-prod-001(f97a229a-2aa9-47e7-ae31-76ed06c11e1d)'
    backendAzureRmResourceGroupName: 'rg-terraformdevops-001'
    backendAzureRmStorageAccountName: 'stterraformdevops01'
    backendAzureRmContainerName: 'terraform'
    backendAzureRmKey: 'y9d6HEg1PDSZBTjxfFG+vN4bctj1qPIHKVnB3a82SMhSJa1bJjvfsloJDw0J5pYzKfVbVVQwBYpC+AStA5P4pw=='
- task: TerraformTaskV4@4
  inputs:
    provider: 'azurerm'
    command: 'validate'
- task: TerraformTaskV4@4
  inputs:
    provider: 'azurerm'
    command: 'apply'
    environmentServiceNameAzureRM: 'bknd-prod-001(1)(f97a229a-2aa9-47e7-ae31-76ed06c11e1d)'
```
# Containerizing an application with Docker

The application will be containerized using Docker, creating a self-contained package with all dependencies. This promotes portability and simplifies deployments.
`INTERMEDIATE` `DOCKER` `LINUX`

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
# Deploying a web application with Kubernetes
Kubernetes will be used to orchestrate the deployment of Docker containers across multiple servers for scalability and high availability.
`ADVANCED` `KUBERNETES` `DOCKER`

```ruby
echo "Creating images..."

docker build -t alemorales9011935/projeto-backend:1.0 backend/.  # Build docker image.
Creates a self-contained executable package for running an application
docker build -t alemorales9011935/projeto-database:1.0 database/. 

echo "Pushing images..."

docker push alemorales9011935/projeto-backend:1.0 # Uploading a completed Docker image to a Docker registry.
docker push alemorales9011935/projeto-database:1.0

echo "Creating Services..."

kubectl apply -f ./services.yml --validate=false # Figure out how to achieve
the desired state of the infrastucture we define.

echo "Criating Deployment"

kubectl apply -f ./deployment.yml --validate=false # Controls the validation behaviour.
```
# Automating Web App deployment with Bash

A Bash script will trigger the Azure DevOps pipeline upon code commit, automating the entire deployment process.
`ADVANCED` `BASH` `LINUX` `AZURE DEVOPS`

```ruby
----------------------------------------------------------------------------------
echo "Updating and installing apache2 and unzip..."
apt-get update
apt-get upgrade -y
apt-get install apache2 -y
apt-get install unzip -y
----------------------------------------------------------------------------------
echo "Getting the website from a remote repo..."
cd /tmp
wget https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip
----------------------------------------------------------------------------------
echo "Unziping the file and pasting into the apache directory..."
unzip main.zip
cd linux-site-dio-main
cp -R * /var/www/html/
----------------------------------------------------------------------------------
```

# Setting developing environment with Vagrant
To provide developers with a consistent local development environment, Vagrant will be used to create virtual machines pre-configured with all the necessary tools and dependencies.
`ADVANCED` `VAGRANT` `IAC`
```ruby
# Creates an object of 3 virtual machines with memory 1024, unique IP and assigns a docker image

machines = {
  "master" => {"memory" => "1024", "cpu" => "1", "ip" => "100", "image" => "bento/ubuntu-22.04"},
  "node01" => {"memory" => "1024", "cpu" => "1", "ip" => "101", "image" => "bento/ubuntu-22.04"},
  "node02" => {"memory" => "1024", "cpu" => "1", "ip" => "102", "image" => "bento/ubuntu-22.04"}
}
# Sets the Vagrant configuration version to "2" 
Vagrant.configure("2") do |config|
```
![Forgeware](images/Forgeware_banner_final.png)

