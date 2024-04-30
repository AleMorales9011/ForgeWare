# Abstract
Janes business Crafty Corner its growing and it time to take it online. In this chapter we will help Jane to design, provision, and manage cloud resources on a chosen cloud platform using Terraform configurations. The project emphasizes best practices for infrastructure as code (IaC) and demonstrates the benefits of managing infrastructure through code.

# Methodology
This repository utilizes a practical learning approach, guiding users through the process of building cloud infrastructure for Crafty Corner on a cloud platform of their choice (e.g., AWS, Google Cloud Platform, Azure). The project will provide step-by-step instructions, explanations for each code block, and troubleshooting tips to ensure a successful learning experience.

# What's Terraform?
Infrastructure as Code (IaC) tools allow you to manage infrastructure with configuration files rather than through a graphical user interface. IaC allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share. 

## Prerequisites:

An Azure subscription (https://azure.microsoft.com/en-us/free)<br>
Terraform installed (https://developer.hashicorp.com/terraform/install)

```ruby
# Terraform Settings Block
terraform {
  required_version = ">= 1.0.0"
  required_providers {
    azurerm = {
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
resource "azurerm_resource_group" "rg-desktop-bknd-001" {
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

# Conclussion

