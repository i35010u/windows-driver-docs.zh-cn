---
title: WDM 简介
description: 若要允许驱动程序开发人员能够编写，跨所有 Microsoft Windows 的源代码兼容操作系统的设备驱动程序，引入了 Windows 驱动程序模型 (WDM)。 遵循 WDM 规则的内核模式驱动程序称为 WDM 驱动程序。
ms.assetid: 00225ec6-fe56-4cbc-b94d-2ba5f28c0bb9
keywords:
- WDM WDK 内核
- Windows 驱动程序模型 WDK 内核
- WDM 驱动程序 WDK 内核
- Wdm.h
- Ntddk.h
- WDM 驱动程序 WDK 内核，有关 WDM 驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba7bc388e9530e90d0d3771c51920841f4fa1b1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575402"
---
# <a name="introduction-to-wdm"></a>WDM 简介


若要使驱动程序开发人员编写设备驱动程序，将源代码兼容跨所有 Microsoft Windows 操作系统中， *Windows 驱动程序模型*(WDM) 引入。 遵循 WDM 规则的内核模式驱动程序被称为*WDM 驱动程序*。




所有 WDM 驱动程序必须都执行以下操作：

-   包括 wdm.h 中，不 Ntddk.h。 （请注意 wdm.h 中是 Ntddk.h 的子集）。

-   设计为总线驱动程序、 功能驱动程序或筛选器驱动程序，如中所述[WDM 驱动程序类型](types-of-wdm-drivers.md)。

-   创建设备对象，如中所述[WDM 设备对象和设备堆栈](wdm-device-objects-and-device-stacks.md)。

-   支持[插即用 (PnP)](implementing-plug-and-play.md)。

-   支持[电源管理](implementing-power-management.md)。

-   支持[Windows Management Instrumentation](implementing-wmi.md) (WMI)。

### <a name="does-the-wdk-cover-non-wdm-drivers"></a>WDK 封面非 WDM 驱动程序？

Windows Driver Kit (WDK) 强调的适用于内核模式的 WDM 驱动程序开发，但 WDK 还包括与内核模式驱动程序不遵循 WDM 规则相关的信息。 此信息可以维护现有的非 WDM 驱动程序和编写新的驱动程序与这些现有的驱动程序连接的。

### <a name="should-you-always-write-a-wdm-driver"></a>您应始终编写 WDM 驱动程序？

如果你正在编写新的内核模式驱动程序，它们应 WDM 驱动程序*除非*你正在编写一个驱动程序，将插入到非 WDM 驱动程序的堆栈。 请阅读设备类型特定于 Microsoft 提供的驱动程序以确定如何新驱动程序的文档必须与 Microsoft 提供的驱动程序。 有关更多的设备特定于类型的信息，请参阅[设备和驱动程序技术](https://msdn.microsoft.com/library/windows/hardware/ff557557)。)

**请注意**  WDM 驱动程序应包含所有新的驱动程序堆栈。

 

跨平台问题，还需要考虑是否正在开发 WDM 或非 WDM 驱动程序。 有关详细信息，请参阅[编写的 Windows 不同版本的驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff554887)。

如果你正在编写新的 WDM 驱动程序，您还应考虑使用[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/dn265580)(KMDF)。 KMDF 提供比 WDM 接口更易于使用的接口。

 

 




