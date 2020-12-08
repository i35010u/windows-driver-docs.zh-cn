---
title: 激活 NDIS 端口
description: 激活 NDIS 端口
keywords:
- 端口 WDK NDIS，激活
- NDIS 端口 WDK，激活
- 激活 NDIS 端口
- 端口状态 WDK NDIS
- 激活 PnP 事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4f1e6341bd5aa9582e5fc4ac3f86aeb1b9f86a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799439"
---
# <a name="activating-an-ndis-port"></a>激活 NDIS 端口





在微型端口驱动程序成功分配 NDIS 端口之后，在 NDIS 函数中使用端口号之前，驱动程序必须激活该端口。 若要激活端口，微型端口驱动程序会将端口激活即插即用 (PnP) 事件发送到 NDIS。 若要发送端口激活 PnP 事件，小型端口驱动程序会在对 [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)函数的调用中使用 **NetEventPortActivation** PnP 事件代码。

若要激活端口，微型端口驱动程序必须将 **NdisMNetPnPEvent** 的 *NetPnPEvent* 参数指向的 [**NET \_ PNP \_ 事件 \_ 通知**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)结构的成员设置为，如下所示：

<a href="" id="portnumber"></a>**PortNumber**  
事件通知的源端口。 将此成员设置为零，因为 **NetPnPEvent** 成员指定的结构的 **Buffer** 成员中提供了端口号。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
描述端口激活事件的 [**NET \_ PNP \_ 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event) 结构。 设置此结构的成员，如下所示：

<a href="" id="netevent"></a>**NetEvent**  
描述事件的事件代码。 将此成员设置为 **NetEventPortActivation**。

<a href="" id="buffer"></a>**宽限**  
指向 [**NDIS \_ 端口**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port) 结构的链接列表的指针。 NDIS 端口结构的 **下一个** 成员 \_ 指向列表中的下一 NDIS \_ 端口结构。

<a href="" id="bufferlength"></a>**BufferLength**  
在 **缓冲区** 中指定的字节数。 将 **BufferLength** 设置为 NDIS \_ 端口结构的大小。

<a href="" id="other-members"></a>其他成员  
将 NET PNP 事件的其余成员设置 \_ \_ 为 **NULL**。

小型小型驱动程序在 [**NDIS \_ 端口**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port) 结构的链接列表中列出了已将状态从非活动更改为活动状态的端口。 但是，如果微型端口适配器的默认端口是 **NetEventPortActivation** PnP 事件的目标，则默认端口必须是列表中的唯一端口。

当微型端口驱动程序将端口 (的激活通知 NDIS，并可能在此通知调用返回) 之前，微型端口驱动程序必须准备好处理与此端口相关联的发送请求和 OID 请求。 微型端口驱动程序不得使用处于状态的新激活端口的端口号，也不能接收指示，直到对 [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) 的调用返回。

在默认端口处于活动状态之前，NDIS 不会通知过量驱动程序已激活的端口。 当 NDIS 调用协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，ndis 会提供 *BindParameters* 参数指向的 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **ActivePorts** 成员中所有当前活动端口的列表。 当微型端口驱动程序激活新端口时，NDIS 会通知所有与 **NetEventPortActivation** PnP 事件绑定到微型端口驱动程序的协议驱动程序。 有关在协议驱动程序中处理这些端口激活事件的详细信息，请参阅 [处理端口激活 PnP 事件](handling-the-port-activation-pnp-event.md)。

在微型端口驱动程序分配 NDIS 端口之前，驱动程序必须调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，以便在 [**ndis \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes) 结构中设置注册属性。 小型端口驱动程序可以通过在 \_ 调用 NdisMSetMiniportAttributes 时设置 NDIS 微型端口 \_ 控件 \_ 默认 \_ 端口属性标志 **NdisMSetMiniportAttributes**，来控制默认端口的激活。 如果微型端口驱动程序假设有责任激活默认端口，则在微型端口驱动程序使用端口激活 PnP 事件激活默认端口之前，NDIS 不会启动微型端口适配器和过量驱动程序之间的绑定。

由 NDIS 端口结构的链接列表指定的所有端口都 \_ 必须处于已分配状态。 微型端口驱动程序不应尝试激活已处于活动状态的端口;如果驱动程序尝试激活活动端口，NDIS 会将这种情况 treates 为端口激活失败。

如果 NDIS 无法激活列表上的任何端口，则无法调用 [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)，并且列表中的任何端口都不会将状态更改为 "已激活" 状态。 如果由于某些端口不存在而导致 NDIS 无法激活端口， **NdisMNetPnPEvent** 将返回 NDIS \_ 状态 " \_ \_ 端口返回值无效"。 如果 NDIS 无法激活端口，因为某些端口未处于已分配状态，则 **NdisMNetPnPEvent** 将返回 NDIS \_ 状态 " \_ \_ 端口 \_ 状态返回值无效"。

成功激活端口后，端口将处于 "已激活" 状态。 小型端口驱动程序可以指示已接收的数据，以及处于激活状态的端口的状态。

NDIS 将默认端口的身份验证状态传递到 [**NDIS \_ 微型端口 \_ 初始化 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)结构的 **DefaultPortAuthStates** 成员的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 如果微型端口驱动程序控制默认端口，当微型端口驱动程序激活默认端口时，它可以通过使用默认的身份验证设置来激活默认端口。 若要使用默认的身份验证设置，请 \_ \_ \_ \_ \_ \_ 在 [**ndis \_ 端口 \_ 特征**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构的 **Flags** 成员中设置 ndis 端口 CHAR "使用默认身份验证设置" 标志。 微型端口驱动程序可以 \_ \_ 对分配和激活的端口使用 NDIS 端口字符 " \_ 使用 \_ 默认 \_ 身份验证 \_ 设置" 标志。 对于激活事例，NDIS 会将默认身份验证状态分配给新激活的端口，并忽略传递给 [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) 的 **NetEventPortActivation** 事件的身份验证状态。

有关控制默认端口和分配端口的详细信息，请参阅 [分配 NDIS 端口](allocating-an-ndis-port.md)。

 

