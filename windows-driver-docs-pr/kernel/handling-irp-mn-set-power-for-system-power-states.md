---
title: 处理 IRP_MN_SET_POWER 的系统电源状态
description: 处理 IRP_MN_SET_POWER 的系统电源状态
ms.assetid: 21e8e8a7-ca77-445b-a49e-28a53f431a26
keywords:
- IRP_MN_SET_POWER
- 系统电源状态 WDK 内核 IRP_MN_SET_POWER
- 设置 power Irp WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36e2048aac516b4420188cbbd383317396f67956
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519785"
---
# <a name="handling-irpmnsetpower-for-system-power-states"></a>处理 IRP\_MN\_设置\_的电源可用于系统的电源状态





电源管理器发送 power 指定少量的代码的 IRP [ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)和出于以下原因之一的系统电源状态：

-   若要更改系统电源状态。

-   若要在故障后重申的当前电源状态[ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)请求。

通过 I/O 管理器中，电源管理器将 IRP 发送到设备堆栈在每个 PnP 设备节点中的顶部驱动程序。 IRP 通知正确的系统电源状态的堆栈中的所有驱动程序。

若要确保有序地启动时，电源管理器序列系统强化 Irp，以便父设备最多有幂的机会，其子项执行操作之前。 电源管理器不会发送一个系统之前查询强化 IRP。

同样，若要确保在计算机睡眠或有序地关闭，电源管理器将发送系统中定义的序列，指定睡眠、 休眠或关机的 Irp，以便在接近根设备之前关闭电源较远的根位置的设备。 只要有可能，电源管理器将查询发送此类 IRP 之前。 有关详细信息，请参阅[处理 IRP\_MN\_查询\_的电源可用于系统的电源状态](handling-irp-mn-query-power-for-system-power-states.md)。

系统电源 IRP 不是直接请求以更改电源状态 — 这是一个通知。 驱动程序不得更改其设备的电源状态为直接回应*系统*IRP; power 驱动程序仅在响应其设备的电源状态更改*设备*power IRP。 (设备电源策略所有者发送设备电源 IRP; 请参阅[处理设备电源策略所有者中系统集 Power IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。)

即使设备已对请求的系统电源状态有效的设备电源状态中，每个驱动程序必须将系统不过传递到下一步低驱动程序，直至到达总线驱动程序集 power IRP。 只有总线驱动程序能够完成此 IRP。

驱动程序处理此 IRP 的方式取决于设备堆栈中其角色以下各节中所述：

[处理设备电源策略所有者中的系统集 Power IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)

[处理系统集 Power IRP 总线驱动程序中](handling-a-system-set-power-irp-in-a-bus-driver.md)

[处理筛选器驱动程序中的系统集 Power IRP](handling-a-system-set-power-irp-in-a-filter-driver.md)

驱动程序不能故障**IRP\_MN\_设置\_POWER**设置系统电源状态请求。 电源管理器将忽略此 IRP 为返回任何失败状态。

 

 




