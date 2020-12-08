---
title: 系统电池管理概述
description: 系统电池管理概述
keywords:
- 电池管理 WDK
- 电池 miniclass 驱动程序 WDK，电池管理
- 电池类型 WDK
- 复合电池驱动程序 WDK
- 电池类驱动程序 WDK，定义
- 电源管理器 WDK 电池
- 电池 GUI WDK
- UPS WDK 电池
- 系统电池管理 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51c752fbf4d4698a3098c2cf6f092ce738ec49e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798677"
---
# <a name="overview-of-system-battery-management"></a>系统电池管理概述


## <span id="ddk_overview_of_system_battery_management_dg"></span><span id="DDK_OVERVIEW_OF_SYSTEM_BATTERY_MANAGEMENT_DG"></span>


电池管理涉及以下系统组件：

-   显示给用户的状态信息，并允许他们设置电池选项的电池 GUI

-   电源管理器

-   复合电池驱动程序，一种由 Microsoft 提供的内核模式驱动程序

-   电池类驱动程序，一种由 Microsoft 提供的内核模式驱动程序

-   单个电池设备的电池 miniclass 驱动程序

-   设备，包括电池和某些不间断电源 (UPS) 

![说明电池管理组件的示意图 ](images/compbatt.png)

由电池 miniclass 驱动程序控制的设备包括电池和某些 UPS 设备。 电池可以是主 (nonrechargeable) 或辅助 (充电) 单元。 从本质上讲，UPS 的容量大得多，并且警报阈值不同于便携式计算机电池。

**注意**   对于连接到 COM 端口的 UPS 设备， [编写 ups 微型驱动程序](writing-ups-minidrivers.md) 最好是为 Windows Vista 之前的操作系统编写电池 miniclass 驱动程序。

 

如上图所示，电池操作中每个组件的角色如下所示：

-   总线驱动程序和一个或多个可选筛选器驱动程序（如 ACPI 筛选器）可能在设备与其 miniclass 驱动程序之间进行分层。

-   *电池 miniclass 驱动程序* 是特定类型的电池或 UPS 设备的函数驱动程序。 系统可以拥有多个电池 miniclass 驱动程序，因为它具有不同类型的电池。

-   *复合电池驱动程序* 跟踪系统中所有电池的状态，并在电源管理器和电池类/miniclass 驱动程序之间充当中介。 复合电池驱动程序从电源管理器接收 Irp，并在电池状态发生变化时通知电源管理器 (例如，当系统电池电量严重不足) 。 复合电池驱动程序与电池类驱动程序的交互方式与电池 miniclass 驱动程序的工作方式几乎相同，但它对其他 miniclass 驱动程序是透明的。 系统有一个组合电池驱动程序，由 Microsoft 提供。

-   *电池类驱动程序* 支持所有电池 miniclass 驱动程序和复合电池驱动程序。 系统具有由 Microsoft 提供的一个电池类驱动程序。

-   *电源管理器* 通过复合电池驱动程序将电源和即插即用 (PnP) irp 发送到电池设备堆栈。 电源管理器不直接与电池类或 miniclass 驱动程序交互;所有 Irp 都是通过复合电池驱动程序发送的。

-   *电池 GUI* 从复合电池驱动程序通过电源管理器获取系统电池状态，并向用户显示该信息。 GUI 还会将 Irp 发送到电池 miniclass 驱动程序，以获取特定于设备的信息。 系统具有由硬件供应商提供的一个电池 GUI。

 

 




