---
title: 创建 Netmap.inf 文件
description: 创建 Netmap.inf 文件
ms.assetid: 0f9b4f57-717c-4f11-b0c6-d117a949ab38
keywords:
- 网络组件升级，WDK，netmap.inf 文件
- 升级网络组件 WDK，netmap.inf 文件
- netmap.inf 文件 WDK
- 供应商提供的文件 WDK netmap.inf 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d05da941108e5db69604c8aeabfaaea786d750e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568777"
---
# <a name="creating-a-netmapinf-file"></a>创建 Netmap.inf 文件





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

Netmap.inf 文件是供应商提供文件中的条目指定的目录中驻留**OemNetUpgradeDirs**一部分[netupg.inf](creating-a-netupg-inf-file.md)文件或目录中，其中包含netupgrd.dll。 Netmap.inf 文件中：

-   映射网络组件的升级前的设备 ID 到该组件的 Microsoft Windows 2000 或更高版本的设备 ID

-   指定网络迁移 NetSetup 加载的 DLL

-   （可选） 指定备用的帮助消息文件

已在 Windows 2000 或更高版本操作系统中内置的升级支持的网络组件不需要供应商提供 netmap.inf 文件，因为这些组件将自动升级在 Windows 2000 和更高版本操作系统的安装过程系统。

本部分包括以下主题：

-   [映射 Netmap.inf 文件中的 Id](mapping-ids-in-a-netmap-inf-file.md)
-   [Netmap.inf 文件中指定升级 DLL](specifying-the-upgrade-dll-in-a-netmap-inf-file.md)
-   [Netmap.inf 文件中指定备用的帮助消息文件](specifying-alternative-help-message-files-in-a-netmap-inf-file.md)

 

 





