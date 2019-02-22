---
title: 处理即插即用事件和中间驱动程序中的电源管理事件
description: 处理即插即用事件和中间驱动程序中的电源管理事件
ms.assetid: 0b4cf76f-a31d-4cf6-8486-090393404af9
keywords:
- 中间驱动程序 WDK 网络事件
- NDIS 中间层驱动程序 WDK，事件
- 即插即用 WDK 网络连接、 中间驱动程序
- 电源管理 WDK 网络连接、 中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3818224c408160c34a8f3b2af0999276ebb4ffa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547138"
---
# <a name="handling-pnp-events-and-power-management-events-in-an-intermediate-driver"></a>处理即插即用事件和中间驱动程序中的电源管理事件





中间的驱动程序必须能够处理插即用 (PnP) 事件和电源管理事件。 特别是：

-   中间的驱动程序必须设置 NDIS\_微型端口\_特性\_否\_暂停\_ON\_中的挂起标志**AttributeFlags**的成员[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构传递给[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)。 有关详细信息，请参阅[初始化为微型端口](initializing-virtual-miniports.md)。

-   中间的驱动程序的虚拟微型端口必须处理 OID\_PNP\_*Xxx*请求。

-   中间的驱动程序的协议部分应传播相应 OID\_PNP\_*Xxx*对基础微型端口驱动程序的请求。 中间驱动程序的虚拟微型端口应传递基础微型端口驱动程序的响应这些请求传回发起请求的协议驱动程序。 中间驱动程序不需要传递请求不需要的设计。 例如，当负载平衡故障转移 (LBFO) 应用程序中没有虚拟微型端口和基础微型端口适配器之间的一对一关系。

-   必须提供中间驱动程序的协议部分[ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)函数。

按任何特定顺序不调用中间驱动程序协议和微型端口事件处理程序。 中间驱动程序的事件处理程序应相应地实现。

本部分包括以下主题：

[初始化句柄 PnP 和电源管理事件的中间驱动程序](initializing-intermediate-drivers-to-handle-pnp-and-power-management-events.md)

[处理 OID\_PNP\_Xxx 查询和集](handling-oid-pnp-xxx-queries-and-sets.md)

[在中间的驱动程序中实现 ProtocolNetPnPEvent 处理程序](implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver.md)

[处理集 Power 请求](handling-a-set-power-request.md)

 

 





