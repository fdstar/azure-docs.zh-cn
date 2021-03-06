---
title: 删除 Azure 自动化混合 Runbook 辅助角色
description: 本文介绍了如何管理已部署的 Azure 自动化混合 Runbook 辅助角色。借助此角色，可以在本地数据中心或云环境中的计算机上运行 Runbook。
services: automation
ms.service: automation
author: georgewallace
ms.author: gwallace
ms.date: 03/19/2018
ms.topic: article
manager: carmonm
ms.openlocfilehash: 0b8f951bbd9712e3d20c3286ef3571e287499c68
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="remove-azure-automation-hybrid-runbook-workers"></a>删除 Azure 自动化混合 Runbook 辅助角色

利用 Azure 自动化的混合 Runbook 辅助角色功能，既可以直接在托管角色的计算机上运行 Runbook，也可以对环境中的资源运行 Runbook，从而管理这些本地资源。 本文将指导你完成从本地计算机中删除混合辅助角色的步骤。

## <a name="removing-hybrid-runbook-worker"></a>删除混合 Runbook 辅助角色

可以从组中删除一个或多个混合 Runbook 辅助角色，或者根据要求删除该组。  若要从本地计算机删除混合 Runbook 辅助角色，请执行以下步骤。

1. 在 Azure 门户中，导航到自动化帐户。  
2. 在“设置”边栏选项卡中，选择“密钥”并记下“URL”和“主访问密钥”字段的值。  下一步需要用到此信息。
3. 在管理员模式下打开 PowerShell 会话，并运行以下命令 - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`。  可使用 **-Verbose** 开关获取删除过程的详细日志。

> [!NOTE]
> 这不会从计算机中删除 Microsoft 监视代理，而只会删除混合 Runbook 辅助角色的功能和配置。  

## <a name="remove-hybrid-worker-groups"></a>删除混合辅助角色组

要删除某个组，首先需要使用前面所示的过程，从每台计算机中删除属于该组的混合 Runbook 辅助角色，然后执行以下步骤删除该组。  

1. 在 Azure 门户中打开自动化帐户。
1. 在“流程自动化”下选择“混合辅助角色组”。 选择要删除的组。  在选择特定的组之后，会显示“混合辅助角色组”属性边栏选项卡。<br> ![混合 Runbook 辅助角色组边栏选项卡](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
2. 在所选组的属性边栏选项卡中，单击“删除”。  此时会显示一条消息请求确认此操作，如果确定要继续，请选择“是”。<br> ![确认删除组对话框](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> 此过程需要几秒钟才能完成，可以在菜单中的“通知”下面跟踪进度。 

## <a name="next-steps"></a>后续步骤

* 查看[在混合 Runbook 辅助角色上运行 Runbook](automation-hrw-run-runbooks.md)，了解如何配置 Runbook，使本地数据中心或其他云环境中的过程实现自动化。
* 若要了解如何安装 Windows 混合 Runbook 辅助角色，请参阅 [Azure 自动化 Windows 混合 Runbook 辅助角色](automation-windows-hrw-install.md)。
* 若要了解如何安装 Linux 混合 Runbook 辅助角色，请参阅 [Azure 自动化 Linux 混合 Runbook 辅助角色](automation-linux-hrw-install.md)。