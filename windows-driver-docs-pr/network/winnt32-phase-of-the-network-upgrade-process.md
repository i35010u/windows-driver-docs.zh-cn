---
title: 网络升级过程的 Winnt32 阶段
description: 网络升级过程的 Winnt32 阶段
keywords:
- 网络组件升级 WDK，阶段
- 升级网络组件 WDK，阶段
- Winnt32.exe 阶段 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 168284ae256dab559ed09bee3f9d6b14fdcf73e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836255"
---
# <a name="winnt32-phase-of-the-network-upgrade-process"></a>网络升级过程的 Winnt32 阶段





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

用户或系统管理员可以通过执行以下任一操作来启动升级过程：

-   选择在 Windows 2000 或更高版本的 CD-ROM 启动后显示的用户界面中的组件升级

-   在 cd-rom 上选择并运行 \\ i386 \\winnt32.exe

如果用户或系统管理员已 \_ \_ \_ 在要升级的系统上设置 NETUPGRD INIT file DIR 环境变量，则 NetSetup 将在该变量指定的目录中搜索 [netupg](creating-a-netupg-inf-file.md) 文件。 Netupg 文件仅包含一个部分： **OemNetUpgradeDirs**。 本部分中的每个条目都指定一个目录的完整路径，该目录包含用于网络组件的供应商提供的升级文件（包括 [netmap](creating-a-netmap-inf-file.md) 文件）。 如果 \_ \_ 未设置 NETUPGRD INIT FILE \_ DIR 环境变量，则 NetSetup ( # A0) 在其自己的目录中查找 netmap 文件。

NetSetup 读取 netmap 文件来识别没有内置升级支持的网络组件。 如果 NetSetup 在无人参与模式下运行，则会显示一个向导;但是，用户或系统管理员不能使用该向导。 如果 NetSetup 未在无人参与模式下运行，则向导将显示没有内置升级支持的网络组件的列表。

用户或系统管理员可以使用该向导执行以下操作：

-   单击 " **取消** " 以中止操作系统的安装。

-   单击 " **下一步** " 以安装操作系统而不升级列出的网络组件。

-   为列出的网络组件指定供应商提供的升级文件的驱动器和目录位置。

    NetSetup 读取指定位置的 netmap 文件，并将该位置的供应商提供的升级文件复制到系统硬盘上的临时目录中。 此临时目录将成为供应商提供的网络迁移 DLL 的工作目录。 NetSetup 还会从向导中的组件列表中删除包含 netmap 文件的任何组件。

NetSetup 在 $Win \_ nt $. ~ bt 目录（通常位于 C：驱动器上） (也称为 AnswerFile) 。

NetSetup 生成 AnswerFile，如下所示：

1.  NetSetup 读取 preupgraded 系统的注册表以枚举每个网络组件。 对于具有内置升级支持的每个网络组件，NetSetup 将从注册表中读取的信息写入 AnswerFile。

2.  对于不具备内置升级支持的每个网络组件，NetSetup 将读取组件的 netmap 文件。 Netmap 文件将网络组件的 preupgrade 设备、硬件或兼容 ID 映射到升级后的操作系统中的相应 ID。 如果 NetSetup 与在 OemNetProtocols 文件的 **OemNetAdapters**、 **OemNetServices**、 **OemAsyncAdapters** 或 **netmap** 部分中使用 preupgrade ID 从注册表读取的网络组件的 preupgrade id 相匹配，NetSetup 会将供应商提供的有关组件的信息写入到 AnswerFile。

3.  使用组件的操作系统设备、硬件或兼容 ID NetSetup 读取 netmap 文件的 **OemUpgradeSupport** 部分，以确定要加载的网络迁移 DLL。 NetSetup 然后加载网络迁移 DLL，并调用 DLL 的 [**PreUpgradeInitialize**](/previous-versions/windows/hardware/network/ff562439(v=vs.85)) 函数。 **PreUpgradeInitialize** 函数提供 DLL 用于初始化自身的信息。

4.  NetSetup 将为网络迁移 DLL 支持的每个网络组件调用一次 DLL 的 [**DoPreUpgradeProcessing**](/previous-versions/windows/hardware/network/ff545634(v=vs.85)) 函数。 **DoPreUpgradeProcessing** 从注册表中读取网络组件的 preupgrade 参数值，并调用 [**NetUpgradeAddSection**](/previous-versions/windows/hardware/network/ff559063(v=vs.85)) 和 [**NetUpgradeAddLineToSection**](/previous-versions/windows/hardware/network/ff559059(v=vs.85)) 函数将这些参数与其他特定于组件的信息一起写入到 AnswerFile。 **DoPreUpgradeProcessing** 还可以通过在 AnswerFile 中做出适当的输入来迁移与 preupgraded 组件关联的二进制数据。

5.  完整生成 AnswerFile 后，NetSetup 会将供应商提供的升级文件复制到相应的目录中，然后启动到升级过程的文本模式阶段。

 

