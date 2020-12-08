---
title: 在 Netmap.inf 文件中指定升级 DLL
description: 在 Netmap.inf 文件中指定升级 DLL
keywords:
- 网络组件升级 WDK，netmap .inf 文件
- 升级网络组件 WDK，netmap .inf 文件
- netmap 文件 WDK
- 升级 DLL WDK netmap
- 设备 Id WDK netmap
- 网络迁移-DLL WDK netmap
- Dll WDK 网络升级
- 供应商提供的文件 WDK netmap 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 008d806b8eefe655a4932dd22c3715e414f876b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815865"
---
# <a name="specifying-the-upgrade-dll-in-a-netmapinf-file"></a>在 Netmap.inf 文件中指定升级 DLL





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

Netmap 文件必须具有 **OemUpgradeSupport** 部分。 对于要升级的每个网络组件， **OemUpgradeSupport** 部分必须包含具有以下格式的条目：

*postupgrade-ID*  = *网络迁移-DLL* \[， *Inf-文件名*\]

其中：

*postupgrade* 是网络组件的 Windows 2000 或更高版本的设备 ID，由 NetSetup 获取，如 [网络升级过程的 winnt32.exe 阶段](winnt32-phase-of-the-network-upgrade-process.md)中所述。

*网络迁移-dll* 是要升级网络组件 NetSetup 必须加载的网络迁移 dll 的名称。 在 netmap 文件中只能指定一个迁移 DLL。 如果 netmap 文件包含多个组件的设备 ID 映射，则必须通过相同的迁移 DLL 升级所有此类组件。

*Inf-* 文件名是安装网络组件的 Inf 文件的名称。

 

 





