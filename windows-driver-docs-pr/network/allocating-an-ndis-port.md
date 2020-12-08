---
title: 分配 NDIS 端口
description: 分配 NDIS 端口
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
ms.openlocfilehash: 76ccdf11ec1d107f09dcdf191c5b38d60d6bb5be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825541"
---
# <a name="allocating-an-ndis-port"></a>分配 NDIS 端口





若要为微型端口适配器分配 NDIS 端口，微型端口驱动程序将调用 [**NdisMAllocatePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport) 函数。 **NdisMAllocatePort** 是同步的，在 NDIS 成功分配端口所需的资源后返回。

在微型端口驱动程序调用 **NdisMAllocatePort** 之前，驱动程序必须调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，以便在 [**NDIS \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes) 结构中设置特性。 在对 **NdisMSetMiniportAttributes** 的调用成功返回后，在 NDIS 为该小型端口适配器调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数之前，微型端口驱动程序可以为微型端口适配器调用 **NdisMAllocatePort** 。

NDIS 始终将默认端口分配 (端口零) 因此小型端口驱动程序不应分配默认端口。 当微型端口驱动程序返回窗体 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)后，NDIS 将释放默认端口。

当微型端口驱动程序调用 [**NdisMAllocatePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)时，NDIS 会将端口号分配给端口。 驱动程序在调用 **NdisMAllocatePort** 之前，在 [**NDIS \_ 端口 \_ 特征**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构中指定了端口特性。 当 **NdisMAllocatePort** 成功返回时， **PortNumber** \_ PortCharacteristics 参数指定的 ndis 端口特征的 PORTNUMBER 成员 \_ 将设置为 ndis 分配给该端口的端口号。 *PortCharacteristics*

从 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)返回之前，微型端口驱动程序必须调用 [**NdisMFreePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport) 函数以释放与微型端口适配器关联的所有端口。 如果微型端口适配器初始化失败，则驱动程序必须调用 **NdisMFreePort** ，以释放驱动程序从 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数返回之前分配的所有端口。 有关释放 NDIS 端口的详细信息，请参阅 [释放 Ndis 端口](freeing-an-ndis-port.md)。

微型端口驱动程序可以分配的最大端口数为0xffffff。 但实际上，驱动程序将设置基于端口类型和驱动程序应用程序要求的最大数目。 例如，对于桥应用程序，端口数量不太可能超过16。 对于使用 802.1 x 请求方端口的访问点而言，端口数量会更高，对于使用虚拟专用网 (VPN) 端口的 WAN 驱动程序，端口数量明显更高。

在微型端口驱动程序分配端口之后，端口将处于已分配状态，并且端口处于非活动状态。 端口不能用于发送和接收数据、启动状态指示、发出 OID 请求，或启动即插即用 (PnP) 事件，直到端口激活。 在微型端口驱动程序设置 [**ndis \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes) 结构中的注册属性后，NDIS 自动激活默认端口。 若要请求 NDIS 不激活默认端口，微型端口驱动程序可以 \_ \_ \_ \_ \_ 在 ndis **AttributeFlags** \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性的 AttributeFlags 成员中设置 ndis 微型端口属性控制默认端口。

NDIS 将默认端口的身份验证状态传递到 [**NDIS \_ 微型端口 \_ 初始化 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构的 **DefaultPortAuthStates** 成员的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 如果微型端口驱动程序控制默认端口，当微型端口驱动程序激活默认端口时，它可以通过使用默认的身份验证设置来激活默认端口。 有关激活默认端口的详细信息，请参阅 [激活 NDIS 端口](activating-an-ndis-port.md)。

小型端口驱动程序可以 \_ \_ \_ \_ \_ \_ 在 [**ndis \_ 端口 \_ 特征**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构的 **Flags** 成员中使用 ndis 端口字符 "使用默认身份验证设置" 标志，以获取驱动程序分配和激活的端口。 对于分配案例，NDIS 会将默认身份验证状态分配给新端口，并忽略传递给 [**NdisMAllocatePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport) 函数的身份验证状态。

有关 NDIS 端口状态的详细信息，请参阅 [Ndis 端口状态](ndis-port-states.md)。 有关激活端口的详细信息，请参阅 [激活 NDIS 端口](activating-an-ndis-port.md)。

 

