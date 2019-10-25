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
ms.openlocfilehash: 658751fc4ec636c06361601ffe9305e0569a1d1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842566"
---
# <a name="handling-pnp-events-and-power-management-events-in-an-intermediate-driver"></a>在中间驱动程序中处理 PnP 事件和电源管理事件





中间驱动程序必须能够处理即插即用（PnP）事件和电源管理事件。 特别是：

-   中间驱动程序必须将 NDIS\_微型端口\_属性\_不\_暂停\_在 [**NDIS\_微型端口\_适配器的 AttributeFlags 成员\_注册\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)传递到[**NDISMSETMINIPORTATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的属性结构。 有关详细信息，请参阅[初始化为微型端口](initializing-virtual-miniports.md)。

-   中间驱动程序的虚拟微型端口必须处理 OID\_PNP\_*Xxx*请求。

-   中间驱动程序的 "协议" 部分应将相应的 OID\_PNP\_*Xxx*请求传播到基础微型端口驱动程序。 中间驱动程序的虚拟微型端口应将基础微型端口驱动程序对这些请求的响应传递回发出请求的协议驱动程序。 中间驱动程序不必传递设计所不需要的请求。 例如，当在负载平衡故障转移（LBFO）应用程序中，虚拟微型端口和基础微型端口适配器之间不存在一对一关系。

-   中间驱动程序的协议部分必须提供[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数。

不按任何特定顺序调用中间驱动程序协议和微型端口事件处理程序。 中间驱动程序的事件处理程序应进行相应的实现。

本部分包括下列主题：

[初始化中间驱动程序以处理 PnP 和电源管理事件](initializing-intermediate-drivers-to-handle-pnp-and-power-management-events.md)

[处理 OID\_PNP\_Xxx 查询和集](handling-oid-pnp-xxx-queries-and-sets.md)

[在中间驱动程序中实现 ProtocolNetPnPEvent 处理程序](implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver.md)

[处理集电源请求](handling-a-set-power-request.md)

 

 





