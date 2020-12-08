---
title: 支持在总线驱动程序中进行 PnP 和电源管理
description: 支持在总线驱动程序中进行 PnP 和电源管理
keywords:
- PnP WDK KMDF，总线驱动程序
- 即插即用 WDK KMDF、总线驱动程序
- 电源管理 WDK KMDF、总线驱动程序
- 总线驱动程序 WDK KMDF
- 子设备 WDK KMDF
- 总线枚举 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90992117336dd5bebc41323bf66d17d28a1ae549
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834845"
---
# <a name="supporting-pnp-and-power-management-in-bus-drivers"></a>支持在总线驱动程序中进行 PnP 和电源管理


某些设备会永久插入系统，而其他设备可以在系统运行时插入并拔出。 *总线驱动程序* 必须识别和报告连接到其总线的设备，并且必须发现并报告系统中设备的到达和出发。

总线驱动程序识别的设备和报告称为总线的 *子设备*。 标识和报告子设备的过程称为 " *总线枚举*"。 在总线枚举过程中，总线驱动程序会为其子设备 [创建设备对象](creating-a-framework-device-object.md) 。 有关总线枚举的详细信息，请参阅 [枚举总线上的设备](enumerating-the-devices-on-a-bus.md)。

总线驱动程序本质上是函数驱动程序，也不是筛选器驱动程序，也处理总线枚举。 总线驱动程序通常是总线适配器的函数驱动程序，但它不是连接到总线的子设备的函数驱动程序。

总线驱动程序还具有功能驱动程序所具有的相同 PnP 和电源管理责任。 有关这些责任的信息，请参阅 [支持功能驱动程序中的 PnP 和电源管理](supporting-pnp-and-power-management-in-function-drivers.md)。

 

 





