---
title: 已知问题和故障排除指南 | Microsoft Docs
description: 已知问题列表和帮助故障排除指南
services: machine-learning
author: svankam
ms.author: svankam
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 01/12/2018
ms.openlocfilehash: db910096f776f2f8710c0ac03f0378491018fc09
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="azure-machine-learning-workbench---known-issues-and-troubleshooting-guide"></a>Azure Machine Learning Workbench - 已知问题和故障排除指南 
作为使用 Azure Machine Learning Workbench 应用程序的一部分，本文帮助你查找和更正错误或遇到的问题。 

## <a name="find-the-workbench-build-number"></a>找到 Workbench 版本号
与支持团队沟通时，请务必提供 Workbench 应用的版本号。 在 Windows 上，可以通过单击“帮助”菜单并选择“关于 Azure ML Workbench”找到版本号。 在 macOS 上，可以单击 **Azure ML Workbench** 菜单，然后选择“关于 Azure ML Workbench”。

## <a name="machine-learning-msdn-forum"></a>机器学习 MSDN 论坛
我们开通了 MSDN 论坛，可以在其上发布问题。 产品团队会主动监视该论坛。 论坛 URL 是 [https://aka.ms/azureml-forum](https://aka.ms/azureml-forum)。 

## <a name="gather-diagnostics-information"></a>收集诊断信息
如果在请求帮助时可以提供诊断信息，有时会很有帮助。 下面是日志文件所在的位置：

### <a name="installer-log"></a>安装程序日志
如果在安装过程中遇到问题，可在此处找到安装程序日志文件：

```
# Windows:
%TEMP%\amlinstaller\logs\*

# macOS:
/tmp/amlinstaller/logs/*
```
可以打包这些目录的内容，然后将它发送给我们进行诊断。

### <a name="workbench-desktop-app-log"></a>Workbench 桌面应用日志
如果登录出现问题或 Workbench 桌面崩溃，可以在此处找到日志文件：
```
# Windows
%APPDATA%\AmlWorkbench

# macOS
~/Library/Application Support/AmlWorkbench
``` 
可以打包这些目录的内容，然后将它发送给我们进行诊断。

### <a name="experiment-execution-log"></a>试验执行日志
如果从桌面应用提交的过程中某个特定脚本执行失败，请尝试通过 CLI 使用 `az ml experiment submit` 命令将其重新提交。 此命令应以 JSON 格式提供完整的错误消息，最重要的是它包含**操作 ID** 值。 请向我们发送包含**操作 ID** 的 JSON 文件，我们可以帮助诊断。 

如果某个特定脚本在提交时成功，但在执行时失败，它应输出**运行 ID** 来标识该特定的运行。 可使用以下命令打包相关日志文件：

```azurecli
# Create a ZIP file that contains all the diagnostics information
$ az ml experiment diagnostics -r <run_id> -t <target_name>
```

`az ml experiment diagnostics` 命令在项目根文件夹中生成 `diagnostics.zip` 文件。 此 ZIP 包包含处于执行时状态的整个项目文件夹，以及日志记录信息。 向我们发送诊断文件之前，请务必删除不想要包含的任何敏感信息。

## <a name="send-us-a-frown-or-a-smile"></a>发送哭脸（或笑脸）

在 Azure ML Workbench 中操作时，还可以单击应用程序 shell 左下角的笑脸图标向我们发送哭脸（或笑脸）。 可以选择性地包含自己的电子邮件地址（以方便我们做出回复）和/或当前状态的屏幕截图。 

## <a name="known-service-limits"></a>已知服务限制
- 允许的最大项目文件夹大小：25 MB。
    >[!NOTE]
    >此限制不适用于 `.git`、`docs` 和 `outputs` 文件夹。 这些文件夹名称区分大小写。 使用大文件时，请参阅[保存更改并处理大文件](../desktop-workbench/how-to-read-write-files.md)。

- 允许的最大试验执行时间：7 天

- 运行后 `outputs` 文件夹中跟踪文件的最大大小：512 MB
  - 这意味着，如果脚本在输出文件夹中生成了大于 512 MB 的文件，则不会收集该文件夹中的文件。 使用大文件时，请参阅[保存更改并处理大文件](../desktop-workbench/how-to-read-write-files.md)。

- 通过 SSH 连接到远程计算机或 Spark 群集时不支持 SSH 密钥。 目前仅支持用户名/密码模式。

- 使用 HDInsight 群集作为计算目标时，它必须使用 Azure blob 作为主存储。 不支持使用 Azure Data Lake 存储。

- Mac 上不支持文本群集转换。

- 只有 Windows 和 Linux 上（Docker 容器中）支持 RevoScalePy 库。 macOS 不支持此库。

- 从 Workbench 应用打开 Jupyter 笔记本时，最大只能打开大小为 5 MB 的笔记本。 可使用“az ml notebook start”命令从 CLI 中打开较大的笔记本，并清除单元输出以减小文件大小。

## <a name="cant-update-workbench"></a>无法更新 Workbench
有新的更新可用时，Workbench 应用主页会显示一条消息，告知有关新更新的信息。 应用左下角的钟形图标上应会显示一条更新锁屏提醒。 单击锁屏提醒并遵照安装向导安装更新。 

![更新映像](./media/known-issues-and-troubleshooting-guide/update.png)

如果未看到通知，请尝试重启应用。 如果重启后仍看不到更新通知，可能有几个原因。

### <a name="you-are-launching-workbench-from-a-pinned-shortcut-on-the-task-bar"></a>Workbench 是通过任务栏上的固定快捷方式启动的
可能已安装更新。 但是，固定的快捷方式仍指向磁盘上的旧软件。 要确认这一点，可以浏览到 `%localappdata%/AmlWorkbench` 文件夹，查看其中是否安装了最新版本，并检查固定快捷方式的属性，以确定其指向哪个位置。 如果已确认，只需删除旧快捷方式，从“开始”菜单启动 Workbench，并根据需要在任务栏中创建新的固定快捷方式。

### <a name="you-installed-workbench-using-the-install-azure-ml-workbench-link-on-a-windows-dsvm"></a>Workbench 是使用 Windows DSVM 上的“安装 Azure ML Workbench”链接安装的
很遗憾，此问题没有简单的解决方法。 必须执行以下步骤删除已安装的软件，并下载最新的安装程序来安装全新的 Workbench： 
   - 删除文件夹 `C:\Users\<Username>\AppData\Local\amlworkbench`
   - 删除脚本 `C:\dsvm\tools\setup\InstallAMLFromLocal.ps1`
   - 删除用于启动上述脚本的桌面快捷方式
   - 下载安装程序 https://aka.ms/azureml-wb-msi 并重新安装。

## <a name="stuck-at-checking-experimentation-account-screen-after-logging-in"></a>登录后停留在“正在检查试验帐户”屏幕
登录后，Workbench 应用可能会停留在空白屏幕上，同时会出现一条消息，显示“正在检查试验帐户”以及一个旋转滚轮。 若要解决此问题，请执行以下步骤：
1. 关闭该应用
2. 删除以下文件：
  ```
  # on Windows
  %appdata%\AmlWorkbench\AmlWb.settings

  # on macOS
  ~/Library/Application Support/AmlWorkbench/AmlWb.settings
  ```
3. 重新启动应用。

## <a name="cant-delete-experimentation-account"></a>无法删除试验帐户
可使用 CLI 删除试验帐户，但是必须先删除这些子工作区内的子工作区和子项目。 否则，会看到“删除嵌套资源前无法删除资源”错误。

```azure-cli
# delete a project
$ az ml project delete -g <resource group name> -a <experimentation account name> -w <worksapce name> -n <project name>

# delete a workspace 
$ az ml workspace delete -g <resource group name> -a <experimentation account name> -n <worksapce name>

# delete an experimentation account
$ az ml account experimentation delete -g <resource group name> -n <experimentation account name>
```

还可以从 Workbench 应用中删除项目和工作区。

## <a name="cant-open-file-if-project-is-in-onedrive"></a>如果项目在 OneDrive 中，则无法打开文件
如果安装了 Windows 10 Fall Creators Update，并且项目是在映射到 OneDrive 的本地文件夹中创建的，则可能无法在 Workbench 中打开任何文件。 原因是 Fall Creators Update 引入的一个 bug 导致 node.js 代码在 OneDrive 文件夹中失败。 我们在不久后会通过 Windows 更新修复该 bug，但在此之前，请不要在 OneDrive 文件夹中创建项目。

## <a name="file-name-too-long-on-windows"></a>Windows 上的文件名太长
如果在 Windows 上使用 Workbench，则可能会遇到最大 260 个字符的默认文件名长度限制，这可能会呈现为“系统找不到指定的路径”错误。 可以修改注册表项设置以允许较长的文件路径名。 查看[本文](https://msdn.microsoft.com/library/windows/desktop/aa365247%28v=vs.85%29.aspx?#maxpath)深入了解如何设置 MAX_PATH 注册表项。

## <a name="interrupt-cli-execution-output"></a>中断 CLI 执行输出
如果使用 `az ml experiment submit` 或 `az ml notebook start` 启动试验运行并且想要中断输出，请执行以下操作： 
- 在 Windows 上，使用键盘中的 Ctrl+Break 组合键
- 在 macOS 上，使用 Ctrl+C。

请注意，这将仅中断 CLI 窗口中的输出流， 不会实际停止正在执行的作业。 如果想要取消正在进行的作业，请使用 `az ml experiment cancel -r <run_id> -t <target name>` 命令。

在键盘中没有 Break 键的 Windows 计算机上，可使用 Fn+B、Ctrl+Fn+B 或 Fn+Esc 替代。请参阅硬件供应商的文档了解特定的组合键。

## <a name="docker-error-read-connection-refused"></a>Docker 错误“读取: 连接被拒绝”
针对本地 Docker 容器执行时，有时可能会出现以下错误： 
```
Get https://registry-1.docker.io/v2/: 
dial tcp: 
lookup registry-1.docker.io on [::1]:53: read udp [::1]:49385->[::1]:53: 
read: connection refused
```

可以通过将 Docker DNS 服务器从 `automatic` 更改为固定值 `8.8.8.8` 来修复此错误。

## <a name="remove-vm-execution-error-no-tty-present"></a>消除 VM 执行错误“不存在 tty”
针对远程 Linux 计算机上的 Docker 容器执行时，可能会遇到以下错误消息：
```
sudo: no tty present and no askpass program specified.
``` 
如果使用 Azure 门户更改 Ubuntu Linux VM 的 root 密码，可能会发生此错误。 

Azure Machine Learning Workbench 需要有无密码 sudoers 访问权限才能在远程主机上运行。 最简单的解决方法是使用 _visudo_ 编辑以下文件（如果不存在该文件，可以创建它）：

```
$ sudo visudo -f /etc/sudoers
```

>[!IMPORTANT]
>必须使用 _visudo_ 而不能使用其他命令编辑该文件。 _visudo_ 会自动对所有 sudo 配置文件执行语法检查，如果无法生成语法正确的 sudoers 文件，可能会将你锁定在 sudo 以外。

在该文件的末尾插入以下行：

```
username ALL=(ALL) NOPASSWD:ALL
```

其中，_username_ 是 Azure Machine Learning Workbench 用来登录远程主机的名称。

必须将该行放在 #includedir "/etc/sudoers.d" 的后面，否则其他规则可能会重写它。

如果使用了更复杂的 sudo 配置，可能需要查阅此处提供的适用于 Ubuntu 的 sudo 文档：https://help.ubuntu.com/community/Sudoers

如果未在 Azure 中使用基于 Ubuntu 的 Linux VM 作为执行目标，也可能会发生上述错误。 仅支持将基于 Ubuntu 的 Linux VM 用于远程执行。 

## <a name="vm-disk-is-full"></a>VM 磁盘已满
在 Azure 中创建新 Linux VM 时，默认会获得 30-GB 的操作系统磁盘。 Docker 引擎默认使用相同的磁盘来提取映像和运行容器。 这可能会填满 OS 磁盘。发生这种情况时，会出现“VM 磁盘已满”错误。

快速解决方法是删除不再使用的所有 Docker 映像。 以下 Docker 命令即可解决此问题。 （当然，必须通过 SSH 连接到 VM 才能通过 bash shell 执行该 Docker 命令。）

```
$ docker system prune -a
```

还可以添加一个数据磁盘，并将 Docker 引擎配置为使用该数据磁盘来存储映像。 了解[如何添加数据磁盘](https://docs.microsoft.com/azure/virtual-machines/linux/add-disk)。 然后，可以[更改 Docker 的映像存储位置](https://forums.docker.com/t/how-do-i-change-the-docker-image-installation-directory/1169)。

或者，可以扩展 OS 磁盘，这样就不需要更改 Docker 引擎配置。 了解[如何扩展 OS 磁盘](https://docs.microsoft.com/azure/virtual-machines/linux/expand-disks)。

```azure-cli
# Deallocate VM (stopping will not work)
$ az vm deallocate --resource-group myResourceGroup  --name myVM

# Get VM's Disc Name
az disk list --resource-group myResourceGroup --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table

# Update Disc Size using above name
$ az disk update --resource-group myResourceGroup --name myVMdisc --size-gb 250
    
# Start VM    
$ az vm start --resource-group myResourceGroup  --name myVM
```

## <a name="sharing-c-drive-on-windows"></a>在 Windows 上共享 C 驱动器
如果在 Windows 上的本地 Docker 容器中执行，在 `docker.compute` 文件中的 `aml_config` 下将 `sharedVolumes` 设置为 `true` 可以改善执行性能。 但是，这需要在“适用于 Windows 的 Docker 工具”中共享 C 驱动器。 如果无法共享 C 驱动器，请尝试遵循以下提示操作：

* 使用文件资源管理器检查 C 驱动器上的共享
* 打开网络适配器设置并为 vEthernet 卸载/重新安装“Microsoft Networks 的文件和打印机共享”
* 打开 Docker 设置并从 Docker 设置内共享 C 驱动器
* Windows 密码的更改会影响共享。 打开文件资源管理器，重新共享 C 驱动器，并输入新密码。
* 尝试在 Docker 中共享 C 驱动器时也可能遇到防火墙问题。 此[堆栈溢出文章](http://stackoverflow.com/questions/42203488/settings-to-windows-firewall-to-allow-docker-for-windows-to-share-drive/43904051)很有帮助。
* 使用域凭据共享 C 驱动器时，对无法访问的域控制器所在的网络，共享可能停止（例如，家庭网络和公共 WiFi 等）。 有关详细信息，请参阅[此文章](https://blogs.msdn.microsoft.com/stevelasker/2016/06/14/configuring-docker-for-windows-volumes/)。

还可以通过在 `docker.compute` 文件中将 `sharedVolumne` 设置为 `false`，以较低的性能代价避免共享问题。

## <a name="wipe-clean-workbench-installation"></a>完全擦除 Workbench 安装
通常不需要执行此操作。 如果必须完全擦除安装，请按照以下步骤进行操作：

- 在 Windows 上：
  - 首选确保使用“控制面板”中的“添加或删除程序”小程序删除“Azure Machine Learning Workbench”应用程序条目。  
  - 然后可下载并运行以下脚本之一：
    - [Windows 命令行脚本](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_win.cmd)。
    - [Windows PowerShell 脚本](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_win.ps1)。 （可能需要先在提升权限的 PowerShell 窗口中运行 `Set-ExecutionPolicy Unrestricted`，然后才能运行该脚本。）
- 在 macOS 上：
  - 只需下载并运行 [macOS bash shell 脚本](https://github.com/Azure/MachineLearning-Scripts/blob/master/cleanup/cleanup_mac.sh)。

## <a name="azure-ml-using-a-different-python-location-than-the-azure-ml-installed-python-environment"></a>Azure 机器学习使用不同的 python 位置，而不是 Azure 机器学习安装的 python 环境
由于 Azure Machine Learning Workbench 最近做了更改，用户可能发现，本地运行可能不再指向 Azure ML Workbench 安装的 python 环境。 如果用户在计算机上安装了另一个 python 环境，并将“Python”路径设置为指向该环境，则可能发生这种情况。 若要使用 Azure ML Workbench 安装的 Python 环境，请执行以下步骤：
- 转到项目根目录下 aml_config 文件夹中的 local.compute 文件。
- 将“pythonLocation”变量更改为指向 Azure ML Workbench 安装的 python 环境的物理路径。 可通过两种方式获取此路径：
    - 可以通过 %Localappdata%\AmlWorkbench\python\python.exe 找到 Azure 机器学习的 python 位置
    - 可在 Azure ML Workbench 中打开 cmd，在命令提示符下键入 python，导入 sys.exe，运行 sys.executable 并从中获取路径。 



## <a name="some-useful-docker-commands"></a>一些有用的 Docker 命令

下面是一些有用的 Docker 命令：

```sh
# display all running containers
$ docker ps

# dislplay all containers (running or stopped)
$ docke ps -a

# display all images
$ docker images

# show Docker logs of a container
$ docker logs <container_id>

# create a new container and launch into a bash shell
$ docker run <image_id> /bin/bash

# launch into a bash shell on a running container
$ docker exec -it <container_id> /bin/bash

# stop an running container
$ docker stop <container_id>

# delete a container
$ docker rm <container_id>

# delete an image
$ docker rmi <image_id>

# delete all unussed Docker images 
$ docker system prune -a

```
