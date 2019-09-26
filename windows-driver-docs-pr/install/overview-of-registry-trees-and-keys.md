---
title: 设备和驱动程序的注册表树
description: 设备和驱动程序的注册表树
ms.assetid: 74dc1889-26a9-47ba-8c8d-3cd6ed95cb68
keywords:
- 硬件密钥 WDK 设备安装
- 注册表 WDK 设备安装
- 软件密钥 WDK 设备安装
- 设备安装 WDK，注册表
- 安装设备 WDK、注册表
- 设备设置 WDK 设备安装，注册表
- 调试设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d64107d1e52dfe83a917dc914e34003357357e
ms.sourcegitcommit: e480dcfea893ef6c85b2dfb5827f51b740466262
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71278372"
---
# <a name="registry-trees-for-devices-and-drivers"></a>设备和驱动程序的注册表树





注册表中的以下树对驱动程序编写者特别感兴趣（其中**HKLM**表示**HKEY_LOCAL_MACHINE**）：

-   [HKLM\\SYSTEM\\CurrentControlSet\\Services 注册表树](hklm-system-currentcontrolset-services-registry-tree.md)

-   [HKLM\\系统\\CurrentControlSet\\控制注册表树](hklm-system-currentcontrolset-control-registry-tree.md)

-   [HKLM\\系统\\CurrentControlSet\\枚举注册表树](hklm-system-currentcontrolset-enum-registry-tree.md)

-   [HKLM\\SYSTEM\\CurrentControlSet\\HardwareProfiles 注册表树](hklm-system-currentcontrolset-hardwareprofiles-registry-tree.md)

有关从 WDF （KMDF 或 UMDF）驱动程序访问注册表项的信息，请参阅[驱动程序的注册表项简介](../wdf/introduction-to-registry-keys-for-drivers.md)。

有关从 WDM 驱动程序访问注册表项的信息，请参阅[即插即用注册表例程](../kernel/plug-and-play-registry-routines.md)。
 

 

 





