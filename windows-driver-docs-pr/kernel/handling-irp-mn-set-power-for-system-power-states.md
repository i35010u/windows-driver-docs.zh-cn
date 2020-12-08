---
title: 处理系统电源状态的 IRP_MN_SET_POWER
description: 处理系统电源状态的 IRP_MN_SET_POWER
keywords:
- IRP_MN_SET_POWER
- 系统电源状态 WDK 内核，IRP_MN_SET_POWER
- 设置电源 Irp WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d90f9ce86ae5435e43e1c4a44ec73bcf1dc40a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836393"
---
# <a name="handling-irp_mn_set_power-for-system-power-states"></a>处理 IRP \_ MN \_ \_ 为系统电源状态设置电源





由于以下原因之一，电源管理器将发送一个指定次要代码 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) 和系统电源状态的电源 IRP：

-   更改系统电源状态。

-   在 [**IRP \_ MN \_ 查询 \_ 电源**](./irp-mn-query-power.md) 请求失败后，重申当前电源状态。

通过 i/o 管理器，电源管理器将 IRP 发送到设备堆栈中每个 PnP 设备节点上的顶层驱动程序。 IRP 通知所有驱动程序处于正确系统电源状态的堆栈中。

为了确保有序启动，电源管理器序列系统开启 Irp，使父设备有机会在其子级之前启动。 在发送系统通电 IRP 之前，电源管理器不会查询。

同样，为确保计算机以有序的方式休眠或关闭，电源管理器会发送系统 Irp，该 Irp 指定以定义的顺序进入睡眠、休眠或关闭状态，以便在设备离根设备之前，设备远离根电源。 在发送此类 IRP 之前，电源管理器会尽可能进行查询。 有关详细信息，请参阅 [处理 IRP \_ MN \_ QUERY \_ Power for System POWER 状态](handling-irp-mn-query-power-for-system-power-states.md)。

系统电源 IRP 不是更改电源状态的直接请求-它是一个通知。 驱动程序不得将其设备的电源状态改为直接响应 *系统* 电源 IRP;驱动程序仅在响应 *设备* 电源 IRP 时更改其设备的电源状态。  (设备电源策略所有者发送设备电源 IRP;请参阅 [在设备电源策略所有者中处理 System Set-Power IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。 ) 

即使设备已处于适用于所请求系统电源状态的设备电源状态，每个驱动程序都必须将系统设置-电源 IRP 传递到下一个较低的驱动程序，直到它到达总线驱动程序。 仅允许总线驱动程序完成此 IRP。

驱动程序处理此 IRP 的方式取决于其在设备堆栈中的角色，如以下部分中所述：

[处理设备电源策略所有者中的系统 Set-Power IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)

[处理总线驱动程序中的系统 Set-Power IRP](handling-a-system-set-power-irp-in-a-bus-driver.md)

[处理筛选器驱动程序中的系统 Set-Power IRP](handling-a-system-set-power-irp-in-a-filter-driver.md)

驱动程序无法使 **IRP \_ MN 设置 \_ 的 \_ 电源** 请求失败，以设置系统电源状态。 Power manager 将忽略为此 IRP 返回的任何故障状态。

 

