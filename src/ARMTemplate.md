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


