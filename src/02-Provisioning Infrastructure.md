# Deploying infrastructure with Terraform

Jane's business Crafty Corner its growing and it's time to take it online, but first she needs **infrastructure to host her website**. In this chapter we will help Jane to **design, provision, and manage** cloud resources on a chosen cloud platform using Terraform configurations.

## Methodology

This file shows fundamental concepts of infrastructure provisioning using Terraform. It leverages HCL, a prevalent language for infrastructure provisioning to build the infrastructure below.

![Infrastructure](https://github.com/AleMorales9011/01-DEVOPS/blob/bf5c286430d93b2bfe3ea4054a73b42836960ece/008%20PROVISIONING%20INFRASTRUCTURE/Backend%20for%20Fronteds%20model.png)

BFF (Back end for frontends pattern)

## Table of contents

- Benefits of using the BFF pattern
- Prerequisites
- What's Terraform
- Installing Terraform
- Installing Azure CLI
- Autenticating with Azure CLI
- Create a Service Principal
- Set your environment variables
- Initialize Terraform
- Write configuration
- Conclussion

## Benefits of using the BFF pattern

- **Improved maintainability:** By separating the backend into multiple services, you can change one service without affecting the others. This makes it easier to develop, test, and deploy changes.
- **Increased scalability:** You can scale each backend service independently to meet the specific needs of the frontend application it serves.
- **Enhanced performance:** By tailoring the backend services to the `specific requirements of each frontend`, you can improve the overall performance of your application

## Prerequisites

An Azure subscription (<https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account>)
Terraform installed (<https://developer.hashicorp.com/terraform/install>)

## What's Terraform?

Infrastructure as Code (IaC) tools allow you to manage infrastructure with configuration files rather than through a graphical user interface.
IaC allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.

## Installing Terraform

To install Terraform, find the [appropriate package for your system](https://developer.hashicorp.com/terraform/install) and download it as a zip archive.

After downloading Terraform, unzip the package. Terraform runs as a single binary named terraform. Any other files in the package can be safely removed and Terraform will still function.

>[!Note]
> Finally, make sure that the terraform binary is available on your ```PATH```. This process will differ depending on your operating system.

## Installing Azure CLI

The Azure CLI will allow you to authenticate with Azure.

```ruby
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi
```

## Autenticating with Azure CLI

Terraform must authenticate to Azure to create infrastructure.

```ruby
az login
```

## Create a Service Principal

Next, we need to create a Service Principal . An application within Azure Active Directory with the authentication tokens Terraform needs to perform actions on your behalf. Update the <SUBSCRIPTION_ID> with the subscription ID you specified in the previous step.

```ruby
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/<SUBSCRIPTION_ID>"
```

## Set your environment variables

A good practice HashiCorp recommends is setting these values as environment variables rather than saving them in your Terraform configuration to avoid passing sensitive info in the configuration code.

```ruby

$Env:ARM_CLIENT_ID = "<APPID_VALUE>"
$Env:ARM_CLIENT_SECRET = "<PASSWORD_VALUE>"
$Env:ARM_SUBSCRIPTION_ID = "<SUBSCRIPTION_ID>"
$Env:ARM_TENANT_ID = "<TENANT_VALUE>"

```

## Initialize Terraform

Initialize the project, which downloads a plugin called a provider that lets Terraform interact with the assigned provider.

```ruby
 terraform init
```

## Write configuration (main.tf)

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

## Variables (var.tf)

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

## Conclussion

By leveraging Terraform's **infrastructure as code (IaC)** approach, you can achieve consistent, repeatable, and version-controlled infrastructure deployments. I encourage you to explore the code, contribute improvements, and leverage this repository as a starting point for your own Terraform journey.
