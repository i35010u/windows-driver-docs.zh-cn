---
title: 自定义网络升级过程
description: 自定义网络升级过程
ms.assetid: c754317c-fe31-4a61-9c73-93ae71f64b03
keywords:
- 网络组件升级 WDK，自定义
- 升级网络组件 WDK、 自定义
- 自定义网络升级过程 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96f90dfa6dc299ee15b426aa4364a2f30a8262d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387373"
---
# <a name="customizing-the-network-upgrade-process"></a>自定义网络升级过程





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

系统管理员可以自定义网络升级过程。

**若要自定义网络升级过程**

1.  要升级的每个网络组件的系统上创建一个目录。

2.  为每个网络组件的供应商提供的升级文件复制到相应步骤 1 中创建的目录。 这些文件必须包括 netmap.inf 文件。 NetSetup 使用 netmap.inf 文件来标识要升级哪些网络组件。

3.  创建包含一个 netupg.inf 文件**OemNetUpgradeDirs**部分，并将其放置所选的目录。 中的每一行**OemNetUpgradeDirs** netupg.inf 文件的部分指定步骤 1 中创建的目录的路径。 Netupg.inf 文件中指定每个目录必须包含有关网络组件，包括 netmap.inf 文件的供应商提供的升级文件。

4.  设置 NET\_UPGRD\_INIT\_文件\_DIR 环境变量为包含 netupg.inf 文件的目录。

在网络升级 Winnt32 阶段，NetSetup netupg.inf 文件在目录中找到指定 NETUPGRD\_INIT\_文件\_DIR 环境变量。 在每个 netupg.inf 文件中指定的目录，NetSetup 然后定位 netmap.inf 文件和网络组件要升级其他供应商文件。 NetSetup 处理这些文件，以升级该组件。 有关详细信息，请参阅[网络升级过程](the-network-upgrade-process.md)。

 

 





