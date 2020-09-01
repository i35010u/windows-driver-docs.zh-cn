---
title: 处理系统电源状态的 IRP_MN_QUERY_POWER
description: 处理系统电源状态的 IRP_MN_QUERY_POWER
ms.assetid: 1904a1cb-a220-41cc-8894-5f90919e7383
keywords:
- IRP_MN_QUERY_POWER
- 系统电源状态 WDK 内核，IRP_MN_QUERY_POWER
- 查询-power Irp WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a6ac17933150da437572fcc4a1757a42664e049
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188289"
---
# <a name="handling-irp_mn_query_power-for-system-power-states"></a>处理 IRP \_ MN \_ QUERY \_ Power For System power 状态





电源管理器使用次要 IRP 代码 [**IRP \_ MN \_ QUERY \_ Power**](./irp-mn-query-power.md) 和 **SystemPowerState** in **Parameters** 发送 power irp，以确定是否可以安全地更改为指定系统电源状态 (S1-S5) 并允许驱动程序准备进行此类更改。

只要有可能，电源管理器就会在发送 [**IRP \_ MN \_ 集 \_ 电源**](./irp-mn-set-power.md) 之前查询，请求 (降低) 状态。 但在电池发生故障或电涌丢失的情况下，电源管理器会发送设置电源 IRP，无需先进行查询。 在发送 IRP 之前，power manager 永远不会发送查询以将系统设置为工作状态 (S0) 。

有关设备的电源策略所有者如何处理系统查询-电源请求的信息，请参阅 [在设备电源策略所有者中处理系统查询-POWER IRP](handling-a-system-query-power-irp-in-a-device-power-policy-owner.md)。

有关不是设备的电源策略所有者) 处理系统查询请求的驱动程序 (的信息，请参阅以下内容：

[处理筛选器或函数驱动程序中的系统 Query-Power IRP](handling-a-system-query-power-irp-in-a-filter-or-function-driver.md)

[使筛选器或函数驱动程序中的系统 Query-Power IRP 失败](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)

[处理总线驱动程序中的系统 Query-Power IRP](handling-a-system-query-power-irp-in-a-bus-driver.md)

请注意，驱动程序决不能发送设备 **IRP \_ MN \_ 设置 \_ 电源** 请求来响应系统查询; 它仅在收到系统设置-电源请求后请求此类 irp。

由于电源管理器会将系统查询 IRP 发送到系统上的每个设备堆栈，因此一个设备的驱动程序可能会导致查询失败，而其他设备的驱动程序可能会成功完成。 从 Windows Vista 开始，系统电源状态到休眠状态的更改是一种关键电源状态更改。 即使驱动程序未通过系统查询-power IRP，Windows Vista 中的电源管理器仍可能会将系统电源状态更改为睡眠状态。 当查询处于活动状态时，也可能是电池过期，需要立即关闭。 因此，在查询 IRP 之后，驱动程序必须准备好接收以下任何电源 Irp：

-   IRP MN 为查询状态** \_ \_ 设置 \_ 电源**

-   **IRP \_ MN \_ 将 \_ 电源设置**为其他电源状态

-   IRP MN 为当前电源状态** \_ \_ 设置 \_ 电源**

-   **IRP \_ MN \_ 查询 \_ **的任何状态

然而，驱动程序通常会在系统查询 IRP 后收到系统集电源 IRP。 无论如何，驱动程序必须准备好更改系统电源状态，即使驱动程序无法进行查询-电源 IRP 也是如此。

 

