---
title: Create training & deploy computes (studio)
titleSuffix: Azure Machine Learning
description: Use studio to create training and deployment compute resources (compute targets) for machine learning
services: machine-learning
author: sdgilley
ms.author: sgilley
ms.reviewer: sgilley
ms.service: machine-learning
ms.subservice: core
ms.date: 10/21/2021
ms.topic: how-to
ms.custom: contperf-fy21q1, sdkv1, event-tier1-build-2022
---
# Create compute targets for model training and deployment in Azure Machine Learning studio

In this article, learn how to create and manage compute targets in Azure Machine studio.  You can also create and manage compute targets with:

* Azure Machine Learning SDK or  CLI extension for Azure Machine Learning
  * [Compute instance](how-to-create-manage-compute-instance.md)
  * [Compute cluster](how-to-create-attach-compute-cluster.md)
  * [Other compute resources](how-to-attach-compute-targets.md)
* The [VS Code extension](how-to-manage-resources-vscode.md#compute-clusters) for Azure Machine Learning.

> [!IMPORTANT]
> Items marked (preview) in this article are currently in public preview.
> The preview version is provided without a service level agreement, and it's not recommended for production workloads. Certain features might not be supported or might have constrained capabilities.
> For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

* If you don't have an Azure subscription, create a free account before you begin. Try the [free or paid version of Azure Machine Learning](https://azure.microsoft.com/free/) today
* An [Azure Machine Learning workspace](how-to-manage-workspace.md)

## What's a compute target? 

With Azure Machine Learning, you can train your model on a variety of resources or environments, collectively referred to as [__compute targets__](v1/concept-azure-machine-learning-architecture.md#compute-targets). A compute target can be a local machine or a cloud resource, such as an Azure Machine Learning Compute, Azure HDInsight, or a remote virtual machine.  You can also create compute targets for model deployment as described in ["Where and how to deploy your models"](how-to-deploy-and-where.md).

## <a id="portal-view"></a>View compute targets

To see all compute targets for your workspace, use the following steps:

1. Navigate to [Azure Machine Learning studio](https://ml.azure.com).
 
1. Under __Manage__, select __Compute__.

1. Select tabs at the top to show each type of compute target.

    :::image type="content" source="media/how-to-create-attach-studio/view-compute-targets.png" alt-text="View list of compute targets":::

## <a id="portal-create"></a>Start creation process

Follow the previous steps to view the list of compute targets. Then use these steps to create a compute target:

1. Select the tab at the top corresponding to the type of compute you will create.

1. If you have no compute targets, select  **Create** in the middle of the page.
  
    :::image type="content" source="media/how-to-create-attach-studio/create-compute-target.png" alt-text="Create compute target":::

1. If you see a list of compute resources, select **+New** above the list.

    :::image type="content" source="media/how-to-create-attach-studio/select-new.png" alt-text="Select new":::


1. Fill out the form for your compute type:

    * [Compute instance](how-to-create-manage-compute-instance.md?tabs=azure-studio#create)
    * [Compute clusters](#amlcompute)
    * [Attached compute](#attached-compute)

1. Select __Create__.

1. View the status of the create operation by selecting the compute target from the list:

    :::image type="content" source="media/how-to-create-attach-studio/view-list.png" alt-text="View compute status from a list":::

Follow the steps in [Create and manage an Azure Machine Learning compute instance](how-to-create-manage-compute-instance.md?tabs=azure-studio#create).


## <a name="amlcompute"></a> Create compute clusters

Create a single or multi node compute cluster for your training, batch inferencing or reinforcement learning workloads. Use the [steps above](#portal-create) to create the compute cluster.  Then fill out the form as follows:

|Field  |Description  |
|---------|---------|
| Location | The Azure region where the compute cluster will be created. By default, this is the same location as the workspace. Setting the location to a different region than the workspace is in __preview__, and is only available for __compute clusters__, not compute instances.</br>When using a different region than your workspace or datastores, you may see increased network latency and data transfer costs. The latency and costs can occur when creating the cluster, and when running jobs on it. |
|Virtual machine type |  Choose CPU or GPU. This type cannot be changed after creation     |
|Virtual machine priority | Choose **Dedicated** or **Low priority**.  Low priority virtual machines are cheaper but don't guarantee the compute nodes. Your job may be preempted.
|Virtual machine size     |  Supported virtual machine sizes might be restricted in your region. Check the [availability list](https://azure.microsoft.com/global-infrastructure/services/?products=virtual-machines)     |

Select **Next** to proceed to **Advanced Settings** and fill out the form as follows:

|Field  |Description  |
|---------|---------|
|Compute name     |  <li>Name is required and must be between 3 to 24 characters long.</li><li>Valid characters are upper and lower case letters, digits, and the  **-** character.</li><li>Name must start with a letter</li><li>Name needs to be unique across all existing computes within an Azure region. You will see an alert if the name you choose is not unique</li><li>If **-**  character is used, then it needs to be followed by at least one letter later in the name</li>     |
|Minimum number of nodes | Minimum number of nodes that you want to provision. If you want a dedicated number of nodes, set that count here. Save money by setting the minimum to 0, so you won't pay for any nodes when the cluster is idle. |
|Maximum number of nodes | Maximum number of nodes that you want to provision. The compute will autoscale to a maximum of this node count when a job is submitted. |
| Idle seconds before scale down | Idle time before scaling the cluster down to the minimum node count. |
| Enable SSH access | Use the same instructions as [Enable SSH access](#enable-ssh) for a compute instance (above). |
|Advanced settings     |  Optional. Configure a virtual network. Specify the **Resource group**, **Virtual network**, and **Subnet** to create the compute instance inside an Azure Virtual Network (vnet). For more information, see these [network requirements](./how-to-secure-training-vnet.md) for vnet.   Also attach [managed identities](#managed-identity) to grant access to resources     |

### <a name="enable-ssh"></a> Enable SSH access

SSH access is disabled by default.  SSH access cannot be changed after creation. Make sure to enable access if you plan to debug interactively with [VS Code Remote](how-to-set-up-vs-code-remote.md).  

[!INCLUDE [amlinclude-info](../../includes/machine-learning-enable-ssh.md)]

Once the compute cluster is created and running, see [Connect with SSH access](#ssh-access).

### <a name="managed-identity"></a> Set up managed identity

[!INCLUDE [aml-clone-in-azure-notebook](../../includes/aml-managed-identity-intro.md)]

During cluster creation or when editing compute cluster details, in the **Advanced settings**, toggle **Assign a managed identity** and specify a system-assigned identity or user-assigned identity.

### Managed identity usage

[!INCLUDE [aml-clone-in-azure-notebook](../../includes/aml-managed-identity-default.md)]

## <a name="inference-clusters"></a> Create inference clusters

> [!IMPORTANT]
> Using Azure Kubernetes Service with Azure Machine Learning has multiple configuration options. Some scenarios, such as networking, require additional setup and configuration. For more information on using AKS with Azure ML, see [Create and attach an Azure Kubernetes Service cluster](how-to-create-attach-kubernetes.md).
Create or attach an Azure Kubernetes Service (AKS) cluster for large scale inferencing. Use the [steps above](#portal-create) to create the AKS cluster.  Then fill out the form as follows:


|Field  |Description  |
|---------|---------|
|Compute name     |  <li>Name is required. Name must be between 2 to 16 characters. </li><li>Valid characters are upper and lower case letters, digits, and the  **-** character.</li><li>Name must start with a letter</li><li>Name needs to be unique across all existing computes within an Azure region. You will see an alert if the name you choose is not unique</li><li>If **-**  character is used, then it needs to be followed by at least one letter later in the name</li>     |
|Kubernetes Service | Select **Create New** and fill out the rest of the form.  Or select **Use existing** and then select an existing AKS cluster from your subscription.
|Region |  Select the region where the cluster will be created |
|Virtual machine size     |  Supported virtual machine sizes might be restricted in your region. Check the [availability list](https://azure.microsoft.com/global-infrastructure/services/?products=virtual-machines)     |
|Cluster purpose  | Select **Production** or **Dev-test** |
|Number of nodes | The number of nodes multiplied by the virtual machine’s number of cores (vCPUs) must be greater than or equal to 12. |
| Network configuration | Select **Advanced** to  create the compute within an existing virtual network. For more information about AKS in a virtual network, see [Network isolation during training and inference with private endpoints and virtual networks](./how-to-secure-inferencing-vnet.md). |
| Enable SSL configuration | Use this to configure SSL certificate on the compute |

## <a name="attached-compute"></a> Attach other compute

To use compute targets created outside the Azure Machine Learning workspace, you must attach them. Attaching a compute target makes it available to your workspace.  Use **Attached compute** to attach a compute target for **training**.  Use **Inference clusters** to attach an AKS cluster for **inferencing**.

Use the [steps above](#portal-create) to attach a compute.  Then fill out the form as follows:

1. Enter a name for the compute target. 
1. Select the type of compute to attach. Not all compute types can be attached from Azure Machine Learning studio. The compute types that can currently be attached for training include:
    * An Azure Virtual Machine (to attach a Data Science Virtual Machine)
    * Azure Databricks (for use in machine learning pipelines)
    * Azure Data Lake Analytics (for use in machine learning pipelines)
    * Azure HDInsight
    * [Kubernetes](./how-to-attach-kubernetes-anywhere.md#attach-a-kubernetes-cluster-to-an-azureml-workspace)

1. Fill out the form and provide values for the required properties.

    > [!NOTE]
    > Microsoft recommends that you use SSH keys, which are more secure than passwords. Passwords are vulnerable to brute force attacks. SSH keys rely on cryptographic signatures. For information on how to create SSH keys for use with Azure Virtual Machines, see the following documents:
    >
    > * [Create and use SSH keys on Linux or macOS](../virtual-machines/linux/mac-create-ssh-keys.md)
    > * [Create and use SSH keys on Windows](../virtual-machines/linux/ssh-from-windows.md)

1. Select __Attach__.

[!INCLUDE [arc-enabled-machine-learning-create-training-compute](../../includes/machine-learning-create-arc-enabled-training-computer-target.md)]

> [!IMPORTANT]
> To attach an Azure Kubernetes Services (AKS) or Azure Arc-enabled Kubernetes cluster, you must be subscription owner or have permission to access AKS cluster resources under the subscription. Otherwise, the cluster list on "attach new compute" page will be blank.

To detach your compute use the following steps:

1. In Azure Machine Learning studio, select __Compute__, __Attached compute__, and the compute you wish to remove.
1. Use the __Detach__ link to detach your compute.

## <a name="ssh-access"></a> Connect with SSH access

If you created your compute instance or compute cluster with SSH access enabled, use these steps for access.

1. Find the compute in your workspace resources:
    1. On the left, select **Compute**.
    1. Use the tabs at the top to select **Compute instance** or **Compute cluster** to find your machine.
1. Select the compute name in the list of resources.
1. Find the connection string:

    * For a **compute instance**, select **Connect** at the top of the **Details** section.

        :::image type="content" source="media/how-to-create-attach-studio/details.png" alt-text="Screenshot: Connect tool at the top of the Details page.":::

    * For a **compute cluster**, select **Nodes** at the top, then select the **Connection string** in the table for your node.
        :::image type="content" source="media/how-to-create-attach-studio/compute-nodes.png" alt-text="Screenshot: Connection string for a node in a compute cluster.":::

1. Copy the connection string.
1. For Windows, open PowerShell or a command prompt:
   1. Go into the directory or folder where your key is stored
   1. Add the -i flag to the connection string to locate the private key and point to where it is stored:
    
      `ssh -i <keyname.pem> azureuser@... (rest of connection string)`

1. For Linux users, follow the steps from [Create and use an SSH key pair for Linux VMs in Azure](../virtual-machines/linux/mac-create-ssh-keys.md)
1. For SCP use: 

   `scp -i key.pem -P {port} {fileToCopyFromLocal }  azureuser@yourComputeInstancePublicIP:~/{destination}`

## Next steps

After a target is created and attached to your workspace, you use it in your [run configuration](how-to-set-up-training-targets.md) with a `ComputeTarget` object:

[!INCLUDE [sdk v1](../../includes/machine-learning-sdk-v1.md)]

```python
from azureml.core.compute import ComputeTarget
myvm = ComputeTarget(workspace=ws, name='my-vm-name')
```

* Use the compute resource to [submit a training run](how-to-set-up-training-targets.md).
* Learn how to [efficiently tune hyperparameters](how-to-tune-hyperparameters.md) to build better models.
* Once you have a trained model, learn [how and where to deploy models](how-to-deploy-and-where.md).
* [Use Azure Machine Learning with Azure Virtual Networks](./how-to-network-security-overview.md)
