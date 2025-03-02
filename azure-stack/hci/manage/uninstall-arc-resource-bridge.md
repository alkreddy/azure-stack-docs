---
title: Uninstall Azure Arc VM management (preview)
description: Learn how to uninstall Azure Arc VM management (preview).
author: ksurjan
ms.author: ksurjan
ms.topic: how-to
ms.service: azure-stack
ms.subservice: azure-stack-hci
ms.custom:
  - devx-track-azurecli
ms.date: 03/23/2022
---

# Uninstall Azure Arc VM management (preview)

[!INCLUDE [hci-applies-to-22h2-21h2](../../includes/hci-applies-to-22h2-21h2.md)]

This article describes how to uninstall Azure Arc VM management on an Azure Arc-enabled Azure Stack HCI cluster.

[!INCLUDE [hci-preview](../../includes/hci-preview.md)]

## How to uninstall Azure Arc VM management

You can set up Azure Arc VM management via [Windows Admin Center](deploy-arc-resource-bridge-using-wac.md) or [Azure Command-Line Interface (CLI)](deploy-arc-resource-bridge-using-command-line.md). However, you can uninstall it only via Azure CLI. You need to set up certain variables when you run the uninstallation commands. For information on how to set up those variables, see [Set up Azure Arc VM management using command line](./deploy-arc-resource-bridge-using-command-line.md).

Perform the following steps to uninstall Azure Arc VM management:

1. Remove the virtual network:

   ```azurecli
   az azurestackhci virtualnetwork delete --subscription $subscription --resource-group $resource_group --name $vnetName --yes
   ```

2. Remove the gallery images:

   ```azurecli
   az azurestackhci galleryimage delete --subscription $subscription --resource-group $resource_group --name $galleryImageName
   ```

3. Remove the custom location:

   ```azurecli
   az customlocation delete --resource-group $resource_group --name $customloc_name --yes
   ```

4. Remove the Kubernetes extension:

   ```azurecli
   az k8s-extension delete --cluster-type appliances --cluster-name $resource_name --resource-group $resource_group --name vmss-hci --yes
   ```

5. Remove the appliance:

   ```azurecli
   az arcappliance delete hci --config-file $csv_path\ResourceBridge\hci-appliance.yaml --yes
   ```

6. Remove the config files:

   ```PowerShell
   Remove-ArcHciConfigFiles
   ```
   > [!NOTE]
   >  The uninstallation of Azure Arc VM management completes at this step.

## Next steps

- [Troubleshoot](troubleshoot-arc-enabled-vms.md)
