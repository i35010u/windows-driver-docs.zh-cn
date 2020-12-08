---
title: 旧式微型端口驱动程序的电源管理
description: 旧式微型端口驱动程序的电源管理
keywords:
- 电源管理 WDK NDIS 微型端口，旧微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e3f9c8444cd3a7214462d6671638f88c5743f57
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806155"
---
# <a name="power-management-for-old-miniport-drivers"></a>旧式微型端口驱动程序的电源管理





NDIS 将微型端口驱动程序视为不能识别电源的旧微型端口驱动程序，前提是：

-   在初始化期间，总线驱动程序指示系统或 NIC 不是电源管理感知。

-   小型端口驱动程序 \_ \_ 在响应 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md) 查询时返回 NDIS 状态。 只有 NDIS 5.1 和更早的微型端口驱动程序或中间驱动程序才会收到此 OID 查询。

-   用户在用户界面中禁用电源管理。

对于不支持 power manegement 的旧微型端口驱动程序，NDIS 仅支持两种设备电源状态：最高功率 (D0) 状态和 D3 状态。

在初始化期间，旧的微型端口驱动程序可以指示在系统转换为睡眠 (D3) 状态之前，NDIS 不应将其暂停。 微型端口驱动程序通过在 \_ \_ \_ \_ \_ 小型端口驱动程序传递给 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的 *AttributeFlags* 参数中设置 NDIS 属性 "不暂停暂停" 标志来进行此类指示。 旧微型端口驱动程序应仅在以下情况下才设置此标志：

-   保存可能需要的所有硬件上下文。

-   将 NIC 置于适当状态，以使休眠状态 (D3) 。

-    (D0) ，将 NIC 重新激活到最高的状态。

如果 NDIS 从总线驱动程序确定 NIC 不能识别电源，并且如果微型端口驱动程序没有 \_ \_ 在挂起标志上设置 NDIS 属性 NO \_ 暂停 \_ \_ ，ndis 将不会查询微型端口驱动程序的电源管理功能。 但是，如果微型端口驱动程序设置 NDIS \_ 属性 \_ " \_ 挂起时不暂停" \_ \_ 标志，ndis 将向微型端口驱动程序发出 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md) 请求。 在这种情况下，微型端口驱动程序应成功完成 OID \_ PNP \_ 功能请求，NDIS \_ 状态为 \_ 成功。 在由 \_ \_ \_ \_ 小型端口驱动程序为响应此请求而返回的 NDIS PM 唤醒功能结构中，微型端口驱动程序还必须为每个唤醒功能指定设备电源状态 **NdisDeviceStateUnspecified** 。

NDIS 为旧微型端口驱动程序提供以下电源管理支持：

-   NDIS 成功将系统电源管理器发送到表示 NIC 的设备对象的所有 [**IRP \_ MN \_ 查询 \_**](../kernel/irp-mn-query-power.md) 请求。 也就是说，NDIS 保证微型端口驱动程序的 NIC 会转换为 D3 状态，以响应系统中的任何 IRP \_ MN \_ 查询 \_ 电源请求。

-   如果微型端口驱动程序未在初始化期间将 NDIS 属性设置为 "暂停时暂停标志"，则在 \_ \_ \_ \_ \_ 微型端口驱动程序的 NIC 转换到状态 D3 之前，NDIS 会调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数。 微型端口驱动程序的 NIC 丢失了所有硬件上下文信息。

-   如果微型端口驱动程序在初始化期间将 NDIS 特性设置为 "暂停时不 \_ 暂停" \_ \_ \_ \_ 标志，则在系统转换到状态 D3 之前，ndis 不会暂停微型端口驱动程序。 相反，NDIS 会向微型端口驱动程序发出 [OID \_ PNP \_ 集 \_ 电源](./oid-pnp-set-power.md) 请求到 D3 状态的请求。 微型端口驱动程序必须保存它使用的所有硬件上下文，并将 NIC 置于适用于 D3 状态的状态。

-   当系统正在转换为 S0 [系统电源状态](../kernel/system-power-states.md)时，如果 ndis 暂停微型端口驱动程序，ndis 将调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数。 如果 NDIS 没有暂停微型端口驱动程序，NDIS 会向微型端口驱动程序发出 OID \_ PNP \_ 设置 \_ 电源请求到 D0 状态。 微型端口驱动程序必须将 NIC 置于适于 D0 状态的状态。

-   如果已停止并重新初始化微型端口驱动程序，NDIS 将通过发出 OID 请求来还原所有合适的微型端口驱动程序设置，如数据包筛选器和多播地址列表。 如果没有暂停小型端口驱动程序，然后重新初始化，微型端口驱动程序必须还原此类设置。

 

