---
title: 在 Azure Active Directory 中创建 Cloud App Discovery 快照报表 | Microsoft Docs
description: 提供有关如何使用 Cloud App Discovery 来查找和管理应用程序、这样做的好处以及其工作原理的信息。
services: active-directory
keywords: cloud app discovery, 管理应用程序
documentationcenter: ''
author: curtand
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 09/22/2017
ms.author: curtand
ms.reviewer: nigu
ms.custom: it-pro
ms.openlocfilehash: ad4591223c72893a4488f5515d8ceb83e0d7f8cf
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="create-cloud-app-discovery-snapshot-reports"></a>创建 Cloud App Discovery 快照报表

在设置自动日志收集器之前，请手动上传日志并让 Cloud App Security 对其进行分析。 如果还没有日志，并且想要查看日志样式的示例，请使用以下过程下载示例日志文件以了解日志应有的样式。

## <a name="to-create-a-snapshot-report"></a>创建快照报表

1. 从组织中的用户通过其访问 Internet 的防火墙和代理服务器收集日志文件。 在流量达到峰值的时间内收集组织中具有代表性的用户活动。
2. 在 [Cloud App Security 菜单栏](https://portal.cloudappsecurity.com)上，依次选择“发现”、“创建快照报表”。
  
  ![创建新的快照报表](./media/cloudappdiscovery-set-up-snapshots/create-snapshot-command.png)
3. 输入**报表名称**和**说明**。
    
  ![新建快照报表](./media/cloudappdiscovery-set-up-snapshots/create-snapshot-form.png)
4. 选择要从中上传日志文件的**数据源**。
5. 验证日志格式，以确保根据可以下载的示例其格式正确。 单击“查看并验证”，并单击“下载示例日志”。 然后将日志与提供的示例进行比较以确保其兼容。
  
  ![验证日志格式](./media/cloudappdiscovery-set-up-snapshots/create-snapshot-verify.png)
  >  [!NOTE]
  > FTP 示例格式在快照和自动上传中受支持，而 syslog 仅在自动上传中受支持。 下载示例日志时会下载示例 FTP 日志。
6. **选择要上传的流量日志**。 一次最多可以上传 20 个文件。 此外，还支持压缩文件和 zip 文件。
  
7. 单击“创建”。 上传完成后，可能需要一些时间对这些文件进行分析。 如果是这样，Cloud App Discovery 会在这些文件准备好时发送电子邮件通知。

8. 选择“管理快照报表”并选择快照报表。
  
  ![快照报表管理](./media/cloudappdiscovery-set-up-snapshots/create-snapshot-manage.png)

## <a name="next-steps"></a>后续步骤

* [开始在 Azure AD 中使用 Cloud App Discovery](cloudappdiscovery-get-started.md)
* [配置用于持续报告的自动日志上传](https://docs.microsoft.com/cloud-app-security/discovery-docker)
* [使用自定义日志分析器](https://docs.microsoft.com/cloud-app-security/custom-log-parser)
