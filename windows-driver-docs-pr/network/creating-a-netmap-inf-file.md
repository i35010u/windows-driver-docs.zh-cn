---
title: 创建 Netmap.inf 文件
description: 创建 Netmap.inf 文件
keywords:
- 网络组件升级 WDK，netmap .inf 文件
- 升级网络组件 WDK，netmap .inf 文件
- netmap 文件 WDK
- 供应商提供的文件 WDK netmap 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fed100d0a42a469d5b567bdbe9dba5bf96d642fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813684"
---
# <a name="creating-a-netmapinf-file"></a>创建 Netmap.inf 文件





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

Netmap 文件是供应商提供的文件，它位于 [netupg](creating-a-netupg-inf-file.md)文件的 **OemNetUpgradeDirs** 部分中的条目所指定的目录中或包含 netupgrd.dll 的目录中。 Netmap 文件：

-   将网络组件的 preupgrade 设备 ID 映射到组件的 Microsoft Windows 2000 或更高版本的设备 ID

-   指定 NetSetup 加载的网络迁移 DLL

-   根据需要指定其他帮助消息文件

在 Windows 2000 或更高版本的操作系统中具有内置升级支持的网络组件不需要供应商提供的 netmap 文件，因为在安装 Windows 2000 和更高版本的操作系统的过程中，这些组件将自动升级。

本节包括下列主题：

-   [Netmap.inf 文件中的映射 ID](mapping-ids-in-a-netmap-inf-file.md)
-   [在 Netmap.inf 文件中指定升级 DLL](specifying-the-upgrade-dll-in-a-netmap-inf-file.md)
-   [在 Netmap.inf 文件中指定备用帮助消息文件](specifying-alternative-help-message-files-in-a-netmap-inf-file.md)

 

 





