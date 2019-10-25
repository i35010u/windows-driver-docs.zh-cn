---
title: 分配 NDIS 端口
description: 分配 NDIS 端口
ms.assetid: 39c77921-5841-40f5-90ba-0fba89b3b55e
keywords:
- 端口 WDK NDIS，分配
- NDIS 端口 WDK，分配
- 分配 NDIS 端口
- 端口 WDK NDIS，最大数量
- NDIS 端口 WDK，最大数量
- 端口的最大端口数 NDIS
- 端口状态 WDK NDIS
- 分配的端口状态 WDK NDIS
- 端口号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 884f3cf5b7657e681e0c64be36f57e3be57dc824
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835325"
---
# <a name="allocating-an-ndis-port"></a>分配 NDIS 端口





若要为微型端口适配器分配 NDIS 端口，微型端口驱动程序将调用[**NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)函数。 **NdisMAllocatePort**是同步的，在 NDIS 成功分配端口所需的资源后返回。

在微型端口驱动程序调用**NdisMAllocatePort**之前，驱动程序必须调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数以便在[**NDIS\_微型端口中设置属性\_适配器\_注册\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构。 在对**NdisMSetMiniportAttributes**的调用成功返回后，在 NDIS 为该小型端口适配器调用[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数之前，微型端口驱动程序可以为微型端口适配器调用**NdisMAllocatePort** 。

NDIS 始终分配默认端口（端口零），因此小型端口驱动程序不应分配默认端口。 当微型端口驱动程序返回窗体[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)后，NDIS 将释放默认端口。

当微型端口驱动程序调用[**NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)时，NDIS 会将端口号分配给端口。 驱动程序在调用**NdisMAllocatePort**之前，在[**NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构中指定了端口特性。 当**NdisMAllocatePort**成功返回时，ndis\_\_端口的**PortNumber**成员将设置为*PortCharacteristics*参数指定的端口号。

从[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)返回之前，微型端口驱动程序必须调用[**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)函数以释放与微型端口适配器关联的所有端口。 如果微型端口适配器初始化失败，则驱动程序必须调用**NdisMFreePort** ，以释放驱动程序从[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数返回之前分配的所有端口。 有关释放 NDIS 端口的详细信息，请参阅[释放 Ndis 端口](freeing-an-ndis-port.md)。

微型端口驱动程序可以分配的最大端口数为0xffffff。 但实际上，驱动程序将设置基于端口类型和驱动程序应用程序要求的最大数目。 例如，对于桥应用程序，端口数量不太可能超过16。 对于使用 802.1 x 申请者端口并对使用虚拟专用网（VPN）端口的 WAN 驱动程序而言，使用 x 请求方端口的访问点，端口数量将会更高。

在微型端口驱动程序分配端口之后，端口将处于已分配状态，并且端口处于非活动状态。 端口不能用于发送和接收数据、启动状态指示、发出 OID 请求或启动即插即用（PnP）事件，直到端口激活。 当微型端口驱动程序在[**NDIS\_微型端口\_适配器\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构中设置注册属性后，ndis 自动激活默认端口。 若要请求 NDIS 不激活默认端口，微型端口驱动程序可以在 NDIS\_微型端口\_适配器的**AttributeFlags**成员中\_默认\_端口\_控件设置 NDIS\_微型端口\_属性\_注册\_特性。

NDIS 将默认端口的身份验证状态传递到[**ndis\_微型\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构**中的** [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 如果微型端口驱动程序控制默认端口，当微型端口驱动程序激活默认端口时，它可以通过使用默认的身份验证设置来激活默认端口。 有关激活默认端口的详细信息，请参阅[激活 NDIS 端口](activating-an-ndis-port.md)。

微型端口驱动程序可以使用 NDIS\_端口\_CHAR\_在[**NDIS\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)的**FLAGS**成员中使用\_默认\_authentication\_设置标志。驱动程序的分配和激活。 对于分配案例，NDIS 会将默认身份验证状态分配给新端口，并忽略传递给[**NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)函数的身份验证状态。

有关 NDIS 端口状态的详细信息，请参阅[Ndis 端口状态](ndis-port-states.md)。 有关激活端口的详细信息，请参阅[激活 NDIS 端口](activating-an-ndis-port.md)。

 

 





