---
title: 自定义网络升级过程
description: 自定义网络升级过程
keywords:
- 网络组件升级 WDK，自定义
- 升级网络组件 WDK，自定义
- 自定义网络升级过程 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b195a01316360bba6296f8a0a0c0e30e60853ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838571"
---
# <a name="customizing-the-network-upgrade-process"></a>自定义网络升级过程





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

系统管理员可以自定义网络升级过程。

**自定义网络升级过程**

1.  为要升级的每个网络组件在系统上创建一个目录。

2.  将每个网络组件提供的供应商提供的升级文件复制到你在步骤1中创建的相应目录。 这些文件必须包含 netmap 文件。 NetSetup 使用 netmap 文件来识别要升级的网络组件。

3.  创建一个 netupg 文件，其中包含一个 **OemNetUpgradeDirs** 节，并将其放置在所选的目录中。 Netupg 文件的 **OemNetUpgradeDirs** 部分中的每行指定在步骤1中创建的目录的路径。 Netupg 文件中指定的每个目录必须包含供应商提供的用于网络组件的升级文件，其中包括 netmap 文件。

4.  将 NET \_ UPGRD \_ INIT \_ FILE \_ DIR 环境变量设置为包含 netupg 文件的目录。

在网络升级的 Winnt32.exe 阶段，NetSetup 将在 NETUPGRD \_ INIT \_ file \_ DIR 环境变量指定的目录中查找 netupg 文件。 在 netupg 文件中指定的每个目录中，NetSetup 随后查找要升级的网络组件的 netmap 文件和其他供应商文件。 NetSetup 处理这些文件来升级组件。 有关详细信息，请参阅 [网络升级过程](the-network-upgrade-process.md)。

 

 





