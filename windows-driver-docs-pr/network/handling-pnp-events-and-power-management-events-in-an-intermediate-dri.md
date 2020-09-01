---
title: 在中间驱动程序中处理 PnP 事件和电源管理事件
description: 在中间驱动程序中处理 PnP 事件和电源管理事件
ms.assetid: 0b4cf76f-a31d-4cf6-8486-090393404af9
keywords:
- 中间驱动程序 WDK 网络，事件
- NDIS 中间驱动程序 WDK，事件
- 即插即用 WDK 网络，中间驱动程序
- 电源管理 WDK 网络，中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 966336feaaf141111e47050d648a0718344a12b2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214744"
---
# <a name="handling-pnp-events-and-power-management-events-in-an-intermediate-driver"></a>在中间驱动程序中处理 PnP 事件和电源管理事件





中间驱动程序必须能够处理即插即用 (PnP) 事件和电源管理事件。 具体来说：

-   中间驱动程序必须 \_ \_ \_ \_ \_ \_ 在传递到[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的[**ndis \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构的**AttributeFlags**成员中设置 ndis 微型端口属性 NO 暂停标志。 有关详细信息，请参阅 [初始化为微型端口](initializing-virtual-miniports.md)。

-   中间驱动程序的虚拟微型端口必须处理 OID \_ PNP \_ *Xxx*请求。

-   中间驱动程序的 "协议" 部分应将相应 \_ 的 OID PNP \_ *Xxx*请求传播到基础微型端口驱动程序。 中间驱动程序的虚拟微型端口应将基础微型端口驱动程序对这些请求的响应传递回发出请求的协议驱动程序。 中间驱动程序不必传递设计所不需要的请求。 例如，当在负载平衡故障转移 (LBFO) 应用程序时，虚拟微型端口和基础微型端口适配器之间不存在一对一关系。

-   中间驱动程序的协议部分必须提供 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。

不按任何特定顺序调用中间驱动程序协议和微型端口事件处理程序。 中间驱动程序的事件处理程序应进行相应的实现。

本节包括下列主题：

[初始化中间驱动程序以处理 PnP 和电源管理事件](initializing-intermediate-drivers-to-handle-pnp-and-power-management-events.md)

[处理 OID \_ PNP \_ Xxx 查询和集](handling-oid-pnp-xxx-queries-and-sets.md)

[在中间驱动程序中实现 ProtocolNetPnPEvent 处理程序](implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver.md)

[处理设置电源请求](handling-a-set-power-request.md)

 

