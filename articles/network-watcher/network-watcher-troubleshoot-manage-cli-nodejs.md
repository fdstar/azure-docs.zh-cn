---
title: 对 Azure 虚拟网络网关和连接进行故障排除 — Azure CLI 1.0 | Microsoft Doc
description: 此页说明如何使用 Azure 网络观察程序对 Azure CLI 1.0 进行故障排除
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: jdial
ms.openlocfilehash: 778b1c52720ad0583c57182d5d09db0d765be52f
ms.sourcegitcommit: ca05dd10784c0651da12c4d58fb9ad40fdcd9b10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a>使用 Azure 网络观察程序 Azure CLI 1.0 对虚拟网络网关和连接进行故障排除

> [!div class="op_single_selector"]
> - [Portal](diagnose-communication-problem-between-networks.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

网络观察程序提供了许多功能，因为它关系到了解 Azure 中的网络资源。 其中一项功能就是资源故障排除。 可以通过门户、PowerShell、CLI 或 REST API 调用资源故障排除。 调用后，网络观察程序会检查虚拟网络网关或连接的运行状况，并返回调查结果。

本文使用适用于 Windows、Mac 和 Linux 的跨平台 Azure CLI 1.0。 

## <a name="before-you-begin"></a>开始之前

此方案假定已按照[创建网络观察程序](network-watcher-create.md)中的步骤创建网络观察程序。

有关支持的网关类型列表，请访问[支持的网关类型](/network-watcher-troubleshoot-overview.md#supported-gateway-types)。

## <a name="overview"></a>概述

“资源故障排除”提供对使用虚拟网络网关和连接时发生的问题进行故障排除的功能。 发出资源故障排除请求时，系统将查询并检查日志。 检查完成后，将返回结果。 资源故障排除请求是长时间运行的请求，可能需要好几分钟才能返回结果。 故障排除日志存储在指定的存储帐户上的容器中。

## <a name="retrieve-a-virtual-network-gateway-connection"></a>检索虚拟网络网关连接

在此示例中，将针对连接运行资源故障排除。 还可以向其传递虚拟网络网关。 以下 cmdlet 将列出资源组中的 vpn 连接。

```azurecli
azure network vpn-connection list -g resourceGroupName
```

还可以运行命令以查看订阅中的连接。

```azurecli
azure network vpn-connection list -s subscription
```

知道连接名称后，可以运行此命令来获取其资源 ID：

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a>创建存储帐户

资源故障排除返回有关资源运行状况的数据，还将日志保存到要查看的存储帐户中。 在此步骤中，我们将创建一个存储帐户（如果存在现有的存储帐户，可以使用它）。

1. 创建存储帐户

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. 获取存储帐户密钥

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. 创建容器

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>运行网络观察程序资源故障排除

使用 `network watcher troubleshoot` cmdlet 对资源进行故障排除。 我们将向该 cmdlet 传递资源组、网络观察程序的名称、连接的 ID、存储帐户 的 ID 以及要在其中存储故障排除结果的 blob 的路径。

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

运行 cmdlet 后，网络观察程序将查看资源以确认运行状况。 它将结果返回到 shell，并将结果的日志存储在指定的存储帐户中。

## <a name="understanding-the-results"></a>了解结果

操作文本提供有关如何解决问题的常规指导。 如果可以对问题采取措施，将提供一个包含更多指导的链接。 如果没有更多指导，响应将提供一个用于建立支持案例的 URL。  有关响应的属性及其包含的内容的详细信息，请访问[网络观察程序故障排除概述](network-watcher-troubleshoot-overview.md)

有关从 Azure 存储帐户下载文件的说明，请参阅[通过 .NET 开始使用 Azure Blob 存储](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。 可以使用的另一个工具是存储资源管理器。 有关存储资源管理器的详细信息可以在此链接中找到：[存储资源管理器](http://storageexplorer.com/)

## <a name="next-steps"></a>后续步骤

如果停止 VPN 连接的设置已更改，请参阅[管理网络安全组](../virtual-network/manage-network-security-group.md)找到可能有问题的网络安全组和安全规则。
