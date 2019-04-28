---
title: 网络升级过程的 Winnt32 阶段
description: 网络升级过程的 Winnt32 阶段
ms.assetid: a83edcfb-e075-4763-8a6a-33879ccf2357
keywords:
- 网络组件升级，WDK 阶段
- 升级网络组件 WDK，阶段
- Winnt32 阶段 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0298b9c63779032a3d3fb80fd2fbef8c3d850aea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342902"
---
# <a name="winnt32-phase-of-the-network-upgrade-process"></a>网络升级过程的 Winnt32 阶段





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

用户或系统管理员通过执行以下操作之一来启动升级过程：

-   在 Windows 2000 或更高版本的 CD-ROM 启动后，将显示在用户界面中选择组件升级

-   选择并运行\\i386\\在 CD-ROM 上的 winnt32.exe

如果用户或系统管理员已设置 NETUPGRD\_INIT\_文件\_DIR 正在升级系统上的环境变量，NetSetup 搜索[netupg.inf](creating-a-netupg-inf-file.md)目录中的文件指定该变量。 Netupg.inf 文件包含只有一个部分：**OemNetUpgradeDirs**。 在本部分中的每个项指定了包含供应商提供升级文件，其中包括的目录的完整路径[netmap.inf](creating-a-netmap-inf-file.md)文件中的，网络组件。 如果 NETUPGRD\_INIT\_文件\_DIR 环境变量未设置，NetSetup (netupgrd.dll) 查找 netmap.inf 文件在其自己的目录中。

NetSetup 读取 netmap.inf 文件，以确定有内置的升级支持的网络组件。 如果 NetSetup 在无人参与模式下运行，它将显示向导;但是，用户或系统管理员不能使用该向导。 如果未在无人参与模式下运行 NetSetup，向导将显示不具有内置的升级支持的网络组件的列表。

使用向导、 用户或系统管理员可以：

-   单击**取消**中止的操作系统安装。

-   单击**下一步**不升级所列出的网络组件的情况下安装操作系统。

-   指定供应商提供的列出网络组件的升级文件的驱动器和目录位置。

    NetSetup 读取 netmap.inf 文件中指定的位置，并将在该位置的供应商提供的升级文件复制到系统的硬盘上的临时目录。 此临时目录将成为供应商提供的网络迁移 DLL 的工作目录。 NetSetup 还会删除任何组件，从向导中的组件列表的 netmap.inf 文件。

NetSetup 生成 winnt.sif 文件 （也称为应答文件） 中 $Win\_nt$。 ~ bt 目录，通常位于 c： 驱动器。

NetSetup 生成应答文件，如下所示：

1.  NetSetup 读取 preupgraded 系统来枚举每个网络组件的注册表。 对于已升级的内置支持每个网络组件，NetSetup 写入到应答文件读取注册表中的信息。

2.  对于不具有内置的升级支持每个网络组件，NetSetup 读取组件的 netmap.inf 文件。 Netmap.inf 文件将升级前的设备、 硬件或网络组件的兼容 ID 映射到已升级的操作系统中相应的 ID。 如果从使用升级前 ID 在注册表中读取的网络组件的升级前的 ID 相匹配 NetSetup **OemNetAdapters**， **OemNetProtocols**， **OemNetServices**，或**OemAsyncAdapters** netmap.inf 文件 NetSetup 的部分将供应商提供的组件的信息写入到应答文件。

3.  使用组件的操作系统设备、 硬件或兼容 ID，NetSetup 读数**OemUpgradeSupport** netmap.inf 文件以确定哪些网络迁移 DLL 加载的部分。 NetSetup 然后加载网络迁移 DLL，并调用的 DLL [ **PreUpgradeInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff562439)函数。 **PreUpgradeInitialize**函数提供的 DLL 使用初始化其自身的信息。

4.  NetSetup 调用的 DLL [ **DoPreUpgradeProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff545634)一次每个网络组件支持的网络迁移 DLL 函数。 **DoPreUpgradeProcessing**读取网络组件的升级前的参数值从注册表和调用[ **NetUpgradeAddSection** ](https://msdn.microsoft.com/library/windows/hardware/ff559063)并[ **NetUpgradeAddLineToSection** ](https://msdn.microsoft.com/library/windows/hardware/ff559059)函数将这些参数，以及其他特定于组件的信息，写入到应答文件。 **DoPreUpgradeProcessing**还可以将迁移应答文件中进行相应的条目与 preupgraded 组件关联的二进制数据。

5.  完全生成应答文件后，NetSetup 将供应商提供的升级文件复制到相应的目录，然后启动升级过程的文本模式阶段进入。

 

 





