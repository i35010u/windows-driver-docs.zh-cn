---
title: 旧式微型端口驱动程序的电源管理
description: 旧式微型端口驱动程序的电源管理
ms.assetid: 676c8c4c-3fd7-4063-a704-2bbfdd03a94e
keywords:
- 电源管理 WDK NDIS 微型端口，旧微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d9c75e3f6e7b337ab656f783ce89091b23ec04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843499"
---
# <a name="power-management-for-old-miniport-drivers"></a>旧式微型端口驱动程序的电源管理





NDIS 将微型端口驱动程序视为不能识别电源的旧微型端口驱动程序，前提是：

-   在初始化期间，总线驱动程序指示系统或 NIC 不是电源管理感知。

-   小型端口驱动程序返回 NDIS\_状态\_响应[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)查询不受支持。 只有 NDIS 5.1 和更早的微型端口驱动程序或中间驱动程序才会收到此 OID 查询。

-   用户在用户界面中禁用电源管理。

对于不支持 power manegement 的旧微型端口驱动程序，NDIS 仅支持两种设备电源状态：最高性能（D0）状态和 D3 状态。

在初始化期间，旧的微型端口驱动程序可以指示在系统转换为睡眠（D3）状态之前，NDIS 不应将其暂停。 微型端口驱动程序通过将 AttributeFlags 参数中的 "NDIS\_属性" 设置为 "\_无\_停止\_\_" 来进行此类指示，而微型端口驱动程序将参数传递给[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数。 旧微型端口驱动程序应仅在以下情况下才设置此标志：

-   保存可能需要的所有硬件上下文。

-   将 NIC 置于休眠状态（D3）的相应状态。

-   将 NIC 重新激活到最高的状态（D0）。

如果 NDIS 从总线驱动程序确定 NIC 不能识别电源，并且如果微型端口驱动程序未将 NDIS\_属性设置\_在\_挂起标志上\_停止\_，NDIS 将不会查询微型端口驱动程序的电源管理功能。 但是，如果微型端口驱动程序将 NDIS\_属性设置\_在\_挂起标志上不\_停止\_，则 NDIS 将向微型端口驱动程序发出[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)请求。 在这种情况下，微型端口驱动程序应成功执行 OID\_PNP\_功能请求，并将 NDIS\_状态\_为 "成功"。 在 NDIS\_PM\_唤醒\_多端口驱动程序为响应此请求而返回的\_功能结构，微型端口驱动程序还必须为每个**NdisDeviceStateUnspecified**指定设备电源状态唤醒功能。

NDIS 为旧微型端口驱动程序提供以下电源管理支持：

-   NDIS 成功完成所有[**IRP\_MN\_QUERY\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)系统电源管理器发送到表示 NIC 的设备对象的电源请求。 也就是说，NDIS 保证微型端口驱动程序的 NIC 会转换为 D3 状态，以响应任何 IRP\_MN\_QUERY\_系统发出的 POWER request。

-   如果微型端口驱动程序未将 NDIS\_属性设置\_在初始化期间\_暂停标志上\_停止\_，NDIS 将在微型端口驱动程序的 NIC 之前调用微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数转换到状态 D3。 微型端口驱动程序的 NIC 丢失了所有硬件上下文信息。

-   如果微型端口驱动程序将 NDIS\_属性设置\_在初始化期间\_暂停标志上\_停止\_，则在系统转换到状态 D3 之前，NDIS 不会暂停微型端口驱动程序。 相反，NDIS 会将微型端口驱动程序作为[OID\_PNP\_设置\_电源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)请求到 D3 状态。 微型端口驱动程序必须保存它使用的所有硬件上下文，并将 NIC 置于适用于 D3 状态的状态。

-   当系统正在转换为 S0[系统电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-states)时，如果 ndis 暂停微型端口驱动程序，ndis 将调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 如果 NDIS 没有暂停微型端口驱动程序，NDIS 会将微型端口驱动程序\_PNP\_设置为 D0 状态\_电源请求。 微型端口驱动程序必须将 NIC 置于适于 D0 状态的状态。

-   如果已停止并重新初始化微型端口驱动程序，NDIS 将通过发出 OID 请求来还原所有合适的微型端口驱动程序设置，如数据包筛选器和多播地址列表。 如果没有暂停小型端口驱动程序，然后重新初始化，微型端口驱动程序必须还原此类设置。

 

 





