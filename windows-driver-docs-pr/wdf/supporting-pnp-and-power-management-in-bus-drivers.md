---
title: 总线驱动程序中支持的即插即用和电源管理
description: 总线驱动程序中支持的即插即用和电源管理
ms.assetid: 35a3d734-7d7e-46ee-aba6-fc6a579d4394
keywords:
- 即插即用 WDK KMDF，总线驱动程序
- 插 WDK KMDF，总线驱动程序
- 电源管理 WDK KMDF，总线驱动程序
- 总线驱动程序 WDK KMDF
- 子设备 WDK KMDF
- 总线枚举 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97d8e6c082ab7fe3e65f5fb8f4682f674c89cf28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544700"
---
# <a name="supporting-pnp-and-power-management-in-bus-drivers"></a>总线驱动程序中支持的即插即用和电源管理


某些设备永久插入到系统，而其他人可插入和拔出系统运行时。 *总线驱动程序*必须标识和报告此设备已连接到其总线，且它们必须发现和报告系统中的抵达和出发的设备。

总线驱动程序标识并报告的设备称为的总线*子设备*。 标识和报告子设备的过程称为*总线枚举*。 总线枚举，总线驱动程序期间[创建设备对象](creating-a-framework-device-object.md)及其子设备。 有关总线枚举的详细信息，请参阅[枚举的总线上设备](enumerating-the-devices-on-a-bus.md)。

总线驱动程序是实质上是函数驱动程序，或很少的筛选器驱动程序，还处理总线枚举。 总线驱动程序通常是总线适配器的功能驱动程序，但它不是连接到该总线的子设备功能驱动程序。

总线驱动程序还具有相同功能的驱动程序具有的 PnP 和电源管理职责。 有关这些责任的信息，请参阅[支持即插即用和功能的驱动程序中的电源管理](supporting-pnp-and-power-management-in-function-drivers.md)。

 

 





