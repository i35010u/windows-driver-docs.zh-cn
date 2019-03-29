---
title: 处理系统电源状态的 IRP_MN_QUERY_POWER
description: 处理系统电源状态的 IRP_MN_QUERY_POWER
ms.assetid: 1904a1cb-a220-41cc-8894-5f90919e7383
keywords:
- IRP_MN_QUERY_POWER
- 系统电源状态 WDK 内核 IRP_MN_QUERY_POWER
- 查询能耗 Irp WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d94e8439c1cd85466bc3473fb1ca923eeb601aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576196"
---
# <a name="handling-irpmnquerypower-for-system-power-states"></a>处理 IRP\_MN\_查询\_的电源可用于系统的电源状态





电源管理器将发送具有细微的 IRP 代码 power IRP [ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)并**SystemPowerState**中**Parameters.Power.Type**以确定是否可以安全地更改到指定的系统电源状态 (S1-S5) 并允许驱动程序，以准备进行此类更改。

只要有可能，在发送前查询电源管理器[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)请求较低 （不太通电） 状态。 但是，在电池故障的情况下或即将断电，电源管理器将发送集 power IRP 而无需首先查询。 电源管理器永远不会发送 IRP 即可使系统处于工作状态 (S0) 之前发送查询。

有关设备的电源策略所有者如何处理系统查询能耗请求的信息，请参阅[处理设备电源策略所有者中系统查询能耗 IRP](handling-a-system-query-power-irp-in-a-device-power-policy-owner.md)。

（不在设备的电源策略所有者） 的驱动程序如何处理系统查询能耗请求有关的信息，请参阅：

[处理系统查询能耗 IRP 中一个筛选器或功能驱动程序](handling-a-system-query-power-irp-in-a-filter-or-function-driver.md)

[失败的系统查询能耗 IRP 中一个筛选器或功能驱动程序](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)

[处理系统查询能耗 IRP 总线驱动程序中](handling-a-system-query-power-irp-in-a-bus-driver.md)

请注意，驱动程序必须永远不会发送设备**IRP\_MN\_设置\_POWER**请求系统查询响应中; 只有在收到系统集 power 请求后，它会请求此类 IRP。

因为电源管理器将发送到系统上每个设备堆栈的系统查询 IRP，就可以一台设备的驱动程序可能会失败的查询，而其他设备的驱动程序成功完成。 从 Windows Vista 开始，对系统电源状态为睡眠状态的更改是关键的电源状态更改。 即使驱动程序出现故障可能仍然会查询能耗 IRP，Windows Vista 中的电源管理器的系统将在系统电源状态更改为睡眠状态。 还有可能，查询处于活动状态，需要立即关闭时，电池可能会过期。 因此后一个查询 IRP，, 驱动程序必须准备好接收任何以下 power Irp:

-   **IRP\_MN\_设置\_POWER**到查询的状态

-   **IRP\_MN\_设置\_POWER**到不同的电源状态

-   **IRP\_MN\_设置\_POWER**的当前电源状态

-   **IRP\_MN\_查询\_POWER**到任意状态

通常情况下，但是，驱动程序收到系统集电源 IRP 遵循系统查询 IRP。 无论如何，驱动程序必须准备好更改系统电源状态，即使该驱动程序失败时查询能耗 IRP。

 

 




