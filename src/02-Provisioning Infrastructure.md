![Image](images/person-creating-online-content-with-their-pets.jpg)

# Deploying infrastructure with Terraform and Azure

30 minutes

Terraform's ability to manage infrastructure as code (IaC) makes it ideal for deploying infrastructure in different environments (development, staging, production) and cloud vendors. Companies can leverage the same configuration files with environment-specific variables, ensuring consistency while allowing for variations between environments and vendors.

# Methodology

This file shows fundamental concepts of infrastructure provisioning using Terraform. It leverages HCL, a prevalent language for infrastructure provisioning to build the infrastructure below.

![Infrastructure](https://github.com/AleMorales9011/01-DEVOPS/blob/bf5c286430d93b2bfe3ea4054a73b42836960ece/008%20PROVISIONING%20INFRASTRUCTURE/Backend%20for%20Fronteds%20model.png)

BFF (Back end for frontend pattern)

# Table of contents

1. Benefits of using the BFF pattern
2. Prerequisites
3. What's Terraform
4. Installing Terraform
5. Installing Azure CLI
6. Authenticating with Azure CLI
7. Create a Service Principal
8. Set your environment variables
9 Initialize Terraform
10. Write configuration
11. Conclusion

# Benefits of using the BFF pattern

A software company might use the Backend for Frontends (BFF) pattern by tailoring data and functionalities to each specific UI(desktop vs mobile), BFF can lead to a more optimized and user-friendly experience for different user groups. It allows to have a backend for each frontend, hence the name BFF.

# Prerequisites

1. An Azure subscription
2. Terraform installed

# What's Terraform?

Infrastructure as Code (IaC) tools allow you to manage infrastructure with configuration files rather than through a graphical user interface.
IaC allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.

A simple

# Installing Terraform

To install Terraform, find the [appropriate package for your system](https://developer.hashicorp.com/terraform/install) and download it as a zip archive.

After downloading Terraform, unzip the package. Terraform runs as a single binary named terraform. Any other files in the package can be safely removed and Terraform will still function.

>[!Note]
> Finally, make sure that the terraform binary is available on your ```PATH```. This process will differ depending on your operating system.

# Installing Azure CLI

The Azure CLI will allow you to authenticate with Azure.

```ruby
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
```

# Autenticating with Azure CLI

Terraform must authenticate to Azure to create infrastructure.

```ruby
az login
```

# Create a Service Principal

Next, we need to create a Service Principal. An application within Azure Active Directory with the authentication tokens Terraform needs to perform actions on your behalf. Update the <SUBSCRIPTION_ID> with the subscription ID you specified in the previous step.

```ruby
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/<SUBSCRIPTION_ID>"
```

# Set your environment variables

A good practice HashiCorp recommends is setting these values as environment variables rather than saving them in your Terraform configuration to avoid passing sensitive info in the configuration code.

```ruby

$Env:ARM_CLIENT_ID = "<APPID_VALUE>"
$Env:ARM_CLIENT_SECRET = "<PASSWORD_VALUE>"
$Env:ARM_SUBSCRIPTION_ID = "<SUBSCRIPTION_ID>"
$Env:ARM_TENANT_ID = "<TENANT_VALUE>"

```

# Initialize Terraform

Initialize the project, which downloads a plugin called a provider that lets Terraform interact with the assigned provider.

```ruby
 terraform init
```

# Write configuration (main.tf)

```ruby
# Terraform Settings Block contains Terraform settings, including the required providers Terraform will use
# to provision your infrastructure.

terraform {
  required_version = ">= 1.0.0"
  required_providers {
    azurerm = {      # A plugin that Terraform uses to create and manage your resources.
      source  = "hashicorp/azurerm"
      version = ">= 2.0" # Optional but recommended in production
    }
  }
}
# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}

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

 # Tags for desktop department
variable "desktop_tags" {
  type = map(string)
  default = {
    Department = "Des FEP Team"
    Environment = "Testing"
    Owner = "John Doe"
    Purpose = "Frontend"

  }
}

 # Tags for mobile department
variable "mobile_tags" {
  type = map(string)
  default = {
    Department = "Mob FEP Team"
    Environment = "Testing"
    Owner = "Jane Doe"
    Purpose = "Frontend"

  }
}

# Create a Storage Account for desktop 
resource "azurerm_storage_account" "stdesktopbknd001" {
  name                      = "stdesktopbknd001"
  resource_group_name       = azurerm_resource_group.rg-desktop-bknd-001.name
  location                  = "westeurope"
  account_kind              = "StorageV2"
  account_tier              = "Standard"
  account_replication_type  = "LRS"
}

# Create a Storage Account for mobile 
resource "azurerm_storage_account" "stmobilebknd001" {
  name                      = "stmobilebknd001"
  resource_group_name       = azurerm_resource_group.rg-mobile-bknd-001.name
  location                  = "westeurope"
  account_kind              = "StorageV2"
  account_tier              = "Standard"
  account_replication_type  = "LRS"
}

# Create a Storage Container for desktop
resource "azurerm_storage_container" "stdesktopui001" {
  name                  = "stdesktopui001"
  storage_account_name  = azurerm_storage_account.stdesktopbknd001.name
}

# Create a Storage Container for mobile
resource "azurerm_storage_container" "stmobileui001" {
  name                  = "stmobileui001"
  storage_account_name  = azurerm_storage_account.stmobilebknd001.name
}

```

# Variables (var.tf)

Variable files separate configuration values from the main Terraform code. This allows to reuse the same Terraform codebase for multiple deployments by simply changing the variable values.

```ruby
variable "location" {
  type = string
  default = "westeurope"
}

variable "tags" {
  type = map
  default = {
      "Ambiente" = "Desenvolvimento"
      "Integracao" = "Processo Devops"
      "Compania" = "Aula Devops"
      "Area" = "Marketing"
    }
}
```

![Infrastructure](https://github.com/AleMorales9011/01-DEVOPS/blob/d6b93bf0c23a8f9d49fb552b3129d0794d37e0de/003-ARCHITECTURE-BFF-PATTERN/003-IMAGES/Resources%20created.jpg)

# Conclusion

By leveraging Terraform's **infrastructure as code (IaC)** approach, you can achieve consistent, repeatable, and version-controlled infrastructure deployments. I encourage you to explore the code, contribute improvements, and leverage this repository as a starting point for your own Terraform journey.

# Next

We will create a CI/CD pipeline with Azure DevOps. 
