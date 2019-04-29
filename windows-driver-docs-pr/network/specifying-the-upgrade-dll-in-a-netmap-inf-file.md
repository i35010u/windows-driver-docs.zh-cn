---
title: 在 Netmap.inf 文件中指定升级 DLL
description: 在 Netmap.inf 文件中指定升级 DLL
ms.assetid: 01735a7d-ee33-427d-befa-7429fd64353b
keywords:
- 网络组件升级，WDK，netmap.inf 文件
- 升级网络组件 WDK，netmap.inf 文件
- netmap.inf 文件 WDK
- 升级 DLL WDK netmap.inf
- 设备 Id WDK netmap.inf
- 网络迁移 DLL WDK netmap.inf
- Dll WDK 网络升级
- 供应商提供的文件 WDK netmap.inf 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 419782188d85fb046e836d9120c5fa8a1725e792
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388119"
---
# <a name="specifying-the-upgrade-dll-in-a-netmapinf-file"></a>在 Netmap.inf 文件中指定升级 DLL





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

Netmap.inf 文件必须具有**OemUpgradeSupport**部分。 为要升级，每个网络组件**OemUpgradeSupport**部分必须包含具有以下格式的条目：

*postupgrade ID* = *网络迁移 DLL* \[ ， *Inf 文件名*\]

其中：

*postupgrade ID*网络组件的 Windows 2000 或更高版本的设备 ID，它通过 NetSetup，获得，如中所述[Winnt32 网络升级过程阶段](winnt32-phase-of-the-network-upgrade-process.md)。

*网络迁移 DLL*网络迁移 NetSetup 升级网络组件，必须加载的 DLL 的名称。 Netmap.inf 文件中，可以指定只有一个迁移 DLL。 如果 netmap.inf 文件包含多个组件的设备 ID 映射，必须通过同一个迁移 DLL 升级所有此类组件。

*Inf 文件名*安装网络组件的 INF 文件的名称。

 

 





