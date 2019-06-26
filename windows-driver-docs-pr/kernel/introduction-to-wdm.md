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
ms.openlocfilehash: daca24ee2473401897f803dbc9c4e3d1e1fff0ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381703"
---
# <a name="introduction-to-wdm"></a>WDM 简介

> [!NOTE]
> 本部分包含 WDM 驱动程序，而现在不再建议的驱动程序模型的指南。 选择驱动程序模型的指导，请参阅[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)。

若要使驱动程序开发人员编写设备驱动程序，将源代码兼容跨所有 Microsoft Windows 操作系统中， *Windows 驱动程序模型*(WDM) 引入。 遵循 WDM 规则的内核模式驱动程序被称为*WDM 驱动程序*。

所有 WDM 驱动程序必须都执行以下操作：

-   包括 wdm.h 中，不 Ntddk.h。 （请注意 wdm.h 中是 Ntddk.h 的子集）。

-   设计为总线驱动程序、 功能驱动程序或筛选器驱动程序，如中所述[WDM 驱动程序类型](types-of-wdm-drivers.md)。

-   创建设备对象，如中所述[WDM 设备对象和设备堆栈](wdm-device-objects-and-device-stacks.md)。

-   支持[插即用 (PnP)](implementing-plug-and-play.md)。

-   支持[电源管理](implementing-power-management.md)。

-   支持[Windows Management Instrumentation](implementing-wmi.md) (WMI)。

### <a name="should-you-write-a-wdm-driver"></a>您应编写 WDM 驱动程序？

如果你正在编写新的驱动程序，请考虑使用[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)(KMDF)。 KMDF 提供比 WDM 接口更易于使用的接口。

不要编写 WDM 驱动程序如果驱动程序插入非 WDM 驱动程序的堆栈。 请阅读设备类型特定于 Microsoft 提供的驱动程序以确定如何新驱动程序的文档必须与 Microsoft 提供的驱动程序。 有关更多的设备特定于类型的信息，请参阅[设备和驱动程序技术](https://docs.microsoft.com/windows-hardware/drivers/)。)



