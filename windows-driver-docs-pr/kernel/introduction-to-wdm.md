---
title: WDM 简介
description: 为了使驱动程序开发人员能够在所有 Microsoft Windows 操作系统中编写源代码兼容的设备驱动程序，引入了 Windows 驱动模型 (WDM) 。 遵循 WDM 规则的内核模式驱动程序称为 WDM 驱动程序。
keywords:
- WDM WDK 内核
- Windows 驱动模型 WDK 内核
- WDM 驱动程序 WDK 内核
- Wdm.h
- Ntddk.h
- WDM 驱动程序 WDK 内核，关于 WDM 驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f05c97a26d458cd6e91bebedff9c55e836492910
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838457"
---
# <a name="introduction-to-wdm"></a>WDM 简介

> [!NOTE]
> 本部分包含有关 WDM 驱动程序的指导，即不再推荐使用的驱动程序模型。 有关选择驱动程序模型的指南，请参阅 [选择驱动程序模型](../gettingstarted/choosing-a-driver-model.md)。

为了使驱动程序开发人员能够在所有 Microsoft Windows 操作系统中编写源代码兼容的设备驱动程序，引入了 *Windows 驱动模型* (WDM) 。 遵循 WDM 规则的内核模式驱动程序称为 *wdm 驱动* 程序。

所有 WDM 驱动程序都必须执行以下操作：

-   包括 Wdm，而不是 Ntddk。  (请注意，Wdm 是 Ntddk 的子集 ) 

-   设计为总线驱动程序、函数驱动程序或筛选器驱动程序，如 [WDM 驱动程序的类型](types-of-wdm-drivers.md)中所述。

-   [创建设备对象](creating-a-device-object.md)

-   支持 [ (PnP) 即插即用 ](introduction-to-plug-and-play.md)。

-   支持 [电源管理](./introduction-to-power-management.md)。

-   支持 (WMI) [Windows Management Instrumentation](implementing-wmi.md) 。

### <a name="should-you-write-a-wdm-driver"></a>是否应该编写 WDM 驱动程序？

如果要编写新的驱动程序，请考虑使用 [内核模式驱动程序框架](../wdf/index.md) (KMDF) 。 KMDF 提供比 WDM 接口更简单的接口。

如果要将驱动程序插入到非 WDM 驱动程序的堆栈中，请不要写入 WDM 驱动程序。 请参阅特定于设备类型的 Microsoft 提供的驱动程序的文档，以确定新的驱动程序必须如何与 Microsoft 提供的驱动程序交互。 有关设备类型特定的详细信息，请参阅 [设备和驱动程序技术](../index.yml)。 ) 
