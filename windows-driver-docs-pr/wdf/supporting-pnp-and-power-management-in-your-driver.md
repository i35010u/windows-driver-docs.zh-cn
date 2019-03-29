---
title: 支持在驱动程序中进行 PnP 和电源管理
description: 支持在驱动程序中进行 PnP 和电源管理
ms.assetid: d9cf987f-d994-4ea9-a467-4b1b8bcdc456
keywords:
- 可以借助 PnP WDK KMDF、 大约 PnP 中基于框架的驱动程序
- 基于框架的驱动程序中大约 PnP 插 WDK KMDF，
- 有关电源管理的电源管理 WDK KMDF
- 设备对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27ac07be5276d71a53713c9d7845e291903e73f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576487"
---
# <a name="supporting-pnp-and-power-management-in-your-driver"></a>支持在驱动程序中进行 PnP 和电源管理


默认情况下，框架将处理系统发送给基于框架的驱动程序的所有 PnP 和电源管理请求。 此外，默认情况下，框架提供的输入/输出请求到功能驱动程序仅当驱动程序的硬件可用并在其工作 (D0) 状态。

在编写基于 framework 的驱动程序时，可以使用很多框架的默认行为以轻松地支持你的设备的即插即用和电源管理功能。 但是，如果使用仅框架的默认 PnP 和电源管理行为所有驱动程序堆栈中的驱动程序，你的设备可能会无法正常工作。 例如，设备的功能驱动程序可能需要启用该设备，当设备进入其工作 (D0) 状态。

因此，framework 设备对象提供了一组事件回调函数和一组对象方法，使基于 framework 的驱动程序，以参与 PnP 和电源管理操作。 这些回调函数和对象方法允许在堆栈提供仅 PnP 和电源管理支持所需的每个驱动程序。

通常情况下，每个驱动程序堆栈中的各种驱动程序是负责支持几个 PnP 和电源管理操作。 驱动程序必须支持的操作取决于你正在编写的驱动程序和设备提供的功能的类型。 您的驱动程序应支持的操作有关的详细信息，请参阅：

-   [仅限软件的驱动程序中支持的即插即用和电源管理](supporting-pnp-and-power-management-in-software-only-drivers.md)
-   [支持功能的驱动程序中的 PnP 和电源管理](supporting-pnp-and-power-management-in-function-drivers.md)

 

 





