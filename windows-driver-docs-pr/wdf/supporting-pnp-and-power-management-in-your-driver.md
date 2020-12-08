---
title: 支持在驱动程序中进行 PnP 和电源管理
description: 支持在驱动程序中进行 PnP 和电源管理
keywords:
- 基于框架的驱动程序中的 pnp WDK KMDF
- 即插即用 WDK KMDF，基于框架的驱动程序中的 PnP
- 电源管理-有关电源管理的 WDK KMDF
- 设备对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f80251858172d623a794ab35ab04449a83126f4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815575"
---
# <a name="supporting-pnp-and-power-management-in-your-driver"></a>支持在驱动程序中进行 PnP 和电源管理


默认情况下，框架将处理系统发送到基于框架的驱动程序的所有 PnP 和电源管理请求。 此外，默认情况下，仅当驱动程序的硬件可用且处于工作状态 (D0) 状态时，框架才向函数驱动程序提供 i/o 请求。

编写基于框架的驱动程序时，你可以使用框架的很多默认行为来轻松支持设备的 PnP 和电源管理功能。 但是，如果驱动程序堆栈中的所有驱动程序只使用框架的默认 PnP 和电源管理行为，则设备可能无法正常工作。 例如，当设备进入工作状态 (D0) 状态时，设备的函数驱动程序可能必须启用设备。

因此，框架设备对象提供一组事件回调函数和一组对象方法，使基于框架的驱动程序能够参与 PnP 和电源管理操作。 利用这些回调函数和对象方法，堆栈中的每个驱动程序都可以仅提供必要的 PnP 和电源管理支持。

通常，驱动程序堆栈中的每个驱动程序都负责支持几个 PnP 和电源管理操作。 驱动程序必须支持的操作取决于要编写的驱动程序的类型和设备提供的功能。 有关驱动程序应支持的操作的详细信息，请参阅：

-   [支持在仅限软件的驱动程序中进行 PnP 和电源管理](supporting-pnp-and-power-management-in-software-only-drivers.md)
-   [支持在功能驱动程序中进行 PnP 和电源管理](supporting-pnp-and-power-management-in-function-drivers.md)

 

 





