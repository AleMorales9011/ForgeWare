# ARM Template
An ARM (Azure Resource Manager) template allows you to define Azure resources declaratively. Below is a simple ARM template for deploying a virtual machine (VM) in Azure.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "resources": [
    {
      "type": "Microsoft.Network/virtualNetworks",
      "apiVersion": "2020-11-01",
      "name": "myVNet",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "10.0.0.0/16"
          ]
        }
      }
    },
    {
      "type": "Microsoft.Network/networkInterfaces",
      "apiVersion": "2020-11-01",
      "name": "myNic",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Network/virtualNetworks', 'myVNet')]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipConfig1",
            "properties": {
              "subnet": {
                "id": "[resourceId('Microsoft.Network/virtualNetworks/subnets', 'myVNet', 'default')]"
              },
              "privateIPAllocationMethod": "Dynamic"
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.Compute/virtualMachines",
      "apiVersion": "2021-03-01",
      "name": "myVM",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Network/networkInterfaces', 'myNic')]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "Standard_DS1_v2"
        },
        "osProfile": {
          "computerName": "myVM",
          "adminUsername": "azureuser",
          "adminPassword": "YourP@ssw0rd!"  // Replace with your password
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "18.04-LTS",
            "version": "latest"
          },
          "osDisk": {
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces', 'myNic')]"
            }
          ]
        }
      }
    }
  ]
}
```

# Key Components:

1. **Virtual Network (VNet)**: Defines a virtual network (`myVNet`) with an address space of `10.0.0.0/16`.
2. **Network Interface (NIC)**: Creates a network interface (`myNic`) attached to the virtual network.
3. **Virtual Machine (VM)**: Deploys a virtual machine (`myVM`) using the **Ubuntu 18.04-LTS** image. It uses the **Standard_DS1_v2** size and is connected to the network interface.

# Steps to Deploy:

1. Save the template in a JSON file (e.g., `azuredeploy.json`).
2. Use the Azure CLI to deploy it:

```bash
   az group create --name myResourceGroup --location eastus
   az deployment group create --resource-group myResourceGroup --template-file azuredeploy.json
```
# Pipeline For Building a .Net App
To create a pipeline for building a .NET application using Azure Pipelines, follow these steps to define the pipeline in a `azure-pipelines.yml` file. This example includes stages for code compilation, running unit tests, packaging the application, and deploying it to Azure App Service or Kubernetes.

# **1. Define the Pipeline Configuration**

Create a file named `azure-pipelines.yml` in the root of your repository with the following content. This example uses Azure Pipelines with YAML configuration.

```yaml
# azure-pipelines.yml

trigger:
- main  # Adjust to the branch you want to trigger the pipeline

pool:
  vmImage: 'ubuntu-latest'  # Use an Ubuntu VM for build tasks; adjust if needed

variables:
  buildConfiguration: 'Release'
  azureSubscription: '<Your-Azure-Subscription>'
  appName: '<Your-App-Service-Name>'
  kubernetesCluster: '<Your-Kubernetes-Cluster>'
  containerRegistry: '<Your-Container-Registry>'
  containerImage: '<Your-Container-Image-Name>'

stages:
- stage: Build
  jobs:
  - job: Build
    steps:
    - task: UseDotNet@2
      inputs:
        packageType: 'sdk'
        version: '7.x'  # Use the appropriate .NET SDK version

    - script: dotnet restore
      displayName: 'Restore NuGet packages'

    - script: dotnet build --configuration $(buildConfiguration)
      displayName: 'Build the project'

    - script: dotnet test --configuration $(buildConfiguration)
      displayName: 'Run unit tests'

- stage: Package
  dependsOn: Build
  jobs:
  - job: Package
    steps:
    - script: dotnet publish --configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)
      displayName: 'Publish the app'

    - task: PublishBuildArtifacts@1
      inputs:
        pathtoPublish: '$(Build.ArtifactStagingDirectory)'
        artifactName: 'drop'
        publishLocation: 'Container'

- stage: DeployToAzureAppService
  dependsOn: Package
  jobs:
  - job: Deploy
    steps:
    - task: AzureRmWebAppDeployment@4
      inputs:
        azureSubscription: $(azureSubscription)
        appName: $(appName)
        package: '$(Pipeline.Workspace)/drop/**/*.zip'  # Adjust if packaging format is different

- stage: DeployToKubernetes
  dependsOn: Package
  jobs:
  - job: Deploy
    steps:
    - task: Docker@2
      inputs:
        command: 'buildAndPush'
        repository: $(containerRegistry)/$(containerImage)
        dockerfile: '**/Dockerfile'
        tags: 'latest'

    - task: Kubernetes@1
      inputs:
        connectionType: 'Kubernetes Service Connection'
        kubernetesServiceEndpoint: $(kubernetesCluster)
        command: 'apply'
        arguments: '-f k8s/deployment.yaml'  # Path to your Kubernetes deployment YAML file
```

# **Explanation of Pipeline Stages**

1. **Build**:
   - **UseDotNet@2**: Sets up the .NET SDK.
   - **dotnet restore**: Restores NuGet packages.
   - **dotnet build**: Compiles the .NET project.
   - **dotnet test**: Runs unit tests.

2. **Package**:
   - **dotnet publish**: Publishes the application to the output directory.
   - **PublishBuildArtifacts@1**: Publishes the build artifacts (e.g., the application package) for deployment.

3. **DeployToAzureAppService**:
   - **AzureRmWebAppDeployment@4**: Deploys the application package to Azure App Service. Adjust the `package` path based on how you package your application.

4. **DeployToKubernetes**:
   - **Docker@2**: Builds and pushes a Docker image to the specified container registry.
   - **Kubernetes@1**: Applies the Kubernetes deployment configuration to deploy the containerized application to the Kubernetes cluster.

# **Additional Steps**

- **Configure Azure Pipelines**: Make sure your Azure DevOps organization has access to your Azure subscription and other resources. Set up the necessary service connections for Azure and Kubernetes in Azure DevOps.

- **Kubernetes Deployment YAML**: Ensure that you have a Kubernetes deployment YAML file (`k8s/deployment.yaml`) that defines how your application should be deployed in Kubernetes.

- **Application Service Configuration**: Ensure that the Azure App Service or Kubernetes cluster is properly configured to handle the deployment and that any environment-specific settings are accounted for.

# Conclussion
This YAML configuration provides a basic pipeline setup. Depending on your specific requirements and application, you may need to adjust the details, such as paths, variables, and deployment strategies.
