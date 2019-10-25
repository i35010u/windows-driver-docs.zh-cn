---
title: 激活 NDIS 端口
description: 激活 NDIS 端口
ms.assetid: 0f3bfda2-8faa-4a92-a76b-0c0c361bd667
keywords:
- 端口 WDK NDIS，激活
- NDIS 端口 WDK，激活
- 激活 NDIS 端口
- 端口状态 WDK NDIS
- 激活 PnP 事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5044fed00c74a9961187ace2fbdc4ed97737916
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835394"
---
# <a name="activating-an-ndis-port"></a>激活 NDIS 端口





在微型端口驱动程序成功分配 NDIS 端口之后，在 NDIS 函数中使用端口号之前，驱动程序必须激活该端口。 若要激活端口，微型端口驱动程序会将端口激活即插即用（PnP）事件发送到 NDIS。 若要发送端口激活 PnP 事件，小型端口驱动程序会在对[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)函数的调用中使用**NetEventPortActivation** PnP 事件代码。

若要激活端口，微型端口驱动程序必须将[**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)的成员设置为**NdisMNetPnPEvent**的*NETPNPEVENT*参数指向的\_通知结构，如下所示：

<a href="" id="portnumber"></a>**PortNumber**  
事件通知的源端口。 将此成员设置为零，因为**NetPnPEvent**成员指定的结构的**Buffer**成员中提供了端口号。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
用于描述端口激活事件的[**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)结构。 设置此结构的成员，如下所示：

<a href="" id="netevent"></a>**NetEvent**  
描述事件的事件代码。 将此成员设置为**NetEventPortActivation**。

<a href="" id="buffer"></a>**宽限**  
指向[**NDIS\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port)结构的链接列表的指针。 NDIS\_端口结构的**下一个**成员指向列表中的下一个 NDIS\_端口结构。

<a href="" id="bufferlength"></a>**BufferLength**  
在**缓冲区**中指定的字节数。 将**BufferLength**设置为 NDIS\_端口结构的大小。

<a href="" id="other-members"></a>其他成员  
将 NET\_PNP\_事件的剩余成员设置为**NULL**。

小型端口驱动程序在[**NDIS\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port)结构的链接列表中列出了已将状态从非活动更改为活动状态的端口。 但是，如果微型端口适配器的默认端口是**NetEventPortActivation** PnP 事件的目标，则默认端口必须是列表中的唯一端口。

当微型端口驱动程序向 NDIS 通知端口（可能在此通知调用返回之前）的激活时，微型端口驱动程序必须准备好处理与此端口相关联的发送请求和 OID 请求。 微型端口驱动程序不得使用处于状态的新激活端口的端口号，也不能接收指示，直到对[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)的调用返回。

在默认端口处于活动状态之前，NDIS 不会通知过量驱动程序已激活的端口。 当 NDIS 调用协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，Ndis 在[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 *ActivePorts 成员中提供了所有当前处于活动状态的端口的列表，BindParameters*参数指向。 当微型端口驱动程序激活新端口时，NDIS 会通知所有与**NetEventPortActivation** PnP 事件绑定到微型端口驱动程序的协议驱动程序。 有关在协议驱动程序中处理这些端口激活事件的详细信息，请参阅[处理端口激活 PnP 事件](handling-the-port-activation-pnp-event.md)。

在微型端口驱动程序分配 NDIS 端口之前，驱动程序必须调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，以便在[**NDIS\_微型端口\_适配器\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)中设置注册属性构造. 小型端口驱动程序可以通过在调用**NdisMSetMiniportAttributes**时将 NDIS\_微型端口\_控件\_默认\_端口属性标志，来控制默认端口的激活。 如果微型端口驱动程序假设有责任激活默认端口，则在微型端口驱动程序使用端口激活 PnP 事件激活默认端口之前，NDIS 不会启动微型端口适配器和过量驱动程序之间的绑定。

由 NDIS\_端口结构的链接列表指定的所有端口都必须处于已分配状态。 微型端口驱动程序不应尝试激活已处于活动状态的端口;如果驱动程序尝试激活活动端口，NDIS 会将这种情况 treates 为端口激活失败。

如果 NDIS 无法激活列表上的任何端口，则无法调用[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)，并且列表中的任何端口都不会将状态更改为 "已激活" 状态。 如果由于某些端口不存在而导致 NDIS 无法激活端口， **NdisMNetPnPEvent**将返回 NDIS\_状态\_无效的\_端口返回值。 如果由于某些端口未处于分配状态，NDIS 无法激活端口， **NdisMNetPnPEvent**将返回 NDIS\_状态\_无效\_端口\_状态返回值。

成功激活端口后，端口将处于 "已激活" 状态。 小型端口驱动程序可以指示已接收的数据，以及处于激活状态的端口的状态。

NDIS 将默认端口的身份验证状态传递到[**ndis\_微型\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构**中的** [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 如果微型端口驱动程序控制默认端口，当微型端口驱动程序激活默认端口时，它可以通过使用默认的身份验证设置来激活默认端口。 若要使用默认的身份验证设置，请将 NDIS\_端口设置\_CHAR\_在[**NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构的**FLAGS**成员中使用\_默认\_AUTH\_设置标志。 微型端口驱动程序可以使用 NDIS\_端口\_CHAR\_为其分配和激活的端口使用\_默认\_身份验证\_设置标志。 对于激活事例，NDIS 会将默认身份验证状态分配给新激活的端口，并忽略传递给[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)的**NetEventPortActivation**事件的身份验证状态。

有关控制默认端口和分配端口的详细信息，请参阅[分配 NDIS 端口](allocating-an-ndis-port.md)。

 

 





