# Configuration Management
In the past chapter we created infrastructure so Jane could take it's business online with a website. Now, she needs a way to make changes such as increase storage, update the operating system, update 3rd party services for better performance etc. This infrastructure changes are very common and time consuming so we will want to make it with the less amount of effort and friction as possible. To do that we can automate this process using Azure Devops.

# Methodology
In this recipe you can find a simple way to automate the infrastructure provisioning and configuration management using YML whiting Azure DevOps. Azure Pipelines provides a comprehensive and flexible solution for automating your software development lifecycle.

```ruby

trigger:
  - main  # This specifies that the pipeline will be triggered whenever there's a push to the main branch of your Git repository.

pool:
  vmImage: ubuntu-latest # Defines the virtual agent pool where the pipeline tasks will be executed.

steps:
- task: TerraformInstaller@1 # Installs a specific version of Terraform
  inputs:
    terraformVersion: 'v1.7.4'

- task: TerraformTaskV4@4 # Executes Terraform commands.
  inputs: # Defines the input parameters for the task
    provider: 'azurerm' # Tells Terraform to use the Azure Resource Manager provider for interacting with Azure resources.
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
# Conclusion
By leveraging Azure Pipelines' features, you can achieve continuous integration and continuous delivery (CI/CD) for your projects, ensuring consistent and reliable deployments. We encourage you to explore the code, customize it for your specific needs, and contribute improvements.  The provided examples showcase common CI/CD workflows, but the possibilities are vast.
