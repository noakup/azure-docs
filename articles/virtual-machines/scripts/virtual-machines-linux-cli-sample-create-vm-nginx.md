---
title: Azure CLI Script Sample - Create a Linux VM with NGINX| Microsoft Docs
description: Azure CLI Script Sample - Create a Linux VM with NGINX
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management

ms.assetid:
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
---

# Create a VM with NGINX

This script creates an Azure Virtual Machine and then uses the Azure Virtual Machine Custom Script Extension to install NGINX. Once the script has been run, a demo website can be reached on the public IP address of the virtual machine.

Before running this script, ensure that a connection with Azure has been created using the `az login` command.

This sample works in a Bash shell. For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines-windows-cli-options.md).

## Sample script

The following script creates the virtual machine and invokes the custom script extension.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## Custom Script Extension

The custom script extension copies this script onto the virtual machine. The script is then run to install and configure an NGINX web server. 

```bash
#!/bin/bash
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## Clean up deployment 

After the script sample has been run, the following command can be used to remove the Resource Group, VM, and all related resources.

```azurecli
az group delete --name myResourceGroup
```

## Script explanation

This script uses the following commands to create a resource group, virtual machine, and all related resources. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Creates the virtual machine. This command also specifies the virtual machine image to be used, and administrative credentials.  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Creates a network security group rule to allow inbound traffic. In this sample, port 80 is opened for HTTP traffic. |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | Adds and runs a virtual machine extension to a VM. In this sample, the custom script extension is used to install NGINX.|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Deletes a resource group including all nested resources. |

## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).

Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../virtual-machines-linux-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
