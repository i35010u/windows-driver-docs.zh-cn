---
title: 系统电池管理概述
description: 系统电池管理概述
ms.assetid: ac34b0e1-e6a4-4e22-9164-6e942c1595b6
keywords:
- 电池管理 WDK
- 电池 miniclass 驱动程序 WDK，电池管理
- 电池类型 WDK
- 复合电池驱动程序 WDK
- 电池类驱动程序 WDK 定义
- 电源管理器 WDK 电池
- 电池 GUI WDK
- UPS WDK 电池
- 系统电池管理 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 952ba366f90c76aaa44f57e126485144a120bf1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335394"
---
# <a name="overview-of-system-battery-management"></a>系统电池管理概述


## <span id="ddk_overview_of_system_battery_management_dg"></span><span id="DDK_OVERVIEW_OF_SYSTEM_BATTERY_MANAGEMENT_DG"></span>


电池管理涉及以下系统组件：

-   电池 GUI，它向用户提供状态信息并允许他们可以设置电池选项

-   电源管理器

-   复合电池驱动程序，由 Microsoft 提供的内核模式驱动程序

-   电池类驱动程序由 Microsoft 提供的内核模式驱动程序

-   单个电池设备的电池 miniclass 驱动程序

-   设备，包括电池和一些不间断电源 (UPS)

![说明的电池管理组件的关系图 ](images/compbatt.png)

由电池 miniclass 驱动程序控制的设备包括电池和一些 UPS 设备。 电池可以是主 (nonrechargeable) 或辅助 （可再充电） 的单元格。 从本质上讲，UPS 是带有较多大的容量和便携式计算机电池比一个不同的警报阈值的系统电池。

**请注意**  连接到 COM 端口的 UPS 单位[编写 UPS 微型驱动程序](writing-ups-minidrivers.md)优于编写 Windows Vista 之前的操作系统的电池 miniclass 驱动程序。

 

在上图中所示，每个组件在电池操作中的角色如下所示：

-   总线驱动程序和一个或多个可选的筛选器驱动程序，如 ACPI 的筛选器，可能会在设备和其 miniclass 驱动程序之间进行分层。

-   一个*电池 miniclass 驱动程序*是电池或 UPS 设备的特定类型的函数驱动程序。 系统可以有任意多个电池 miniclass 驱动程序因为它具有不同类型的电池。

-   *复合电池驱动程序*跟踪系统中的所有电池的状态并且可作为电源管理器与电池类/miniclass 驱动程序之间的中介。 复合电池驱动程序从电源管理器接收 Irp 和电池状态发生更改 （例如，当系统电池电量变得严重不足） 时通知电源管理器。 复合电池驱动程序交互使用电池类驱动程序中同样地，电池 miniclass 驱动程序执行，但它是透明的其他 miniclass 驱动程序。 系统具有一个复合电池驱动程序，由 Microsoft 提供。

-   *电池类驱动程序*支持所有电池 miniclass 驱动程序和复合电池驱动程序。 系统具有一个电池类驱动程序，由 Microsoft 提供。

-   *电源管理器*将电源和插即用 (PnP) Irp 发送到电池设备堆栈通过复合电池驱动程序。 电源管理器不直接与电池类或 miniclass 驱动程序; 交互通过复合电池驱动程序发送的所有 Irp。

-   *电池 GUI*电源管理器通过从复合电池驱动程序获取系统电池状态，并向用户呈现信息。 GUI 还将 Irp 发送到特定于设备的信息的电池 miniclass 驱动程序。 系统具有一个电池 GUI，由硬件供应商提供。

 

 




