---
title: 停用 NDIS 端口
description: 停用 NDIS 端口
keywords:
- 端口 WDK NDIS，停用
- NDIS 端口 WDK，停用
- 停用 NDIS 端口 WDK NDIS
- 停用 PnP 事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49c980ae7d98c32f95c8b0c828ddf87ccf52f24b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814971"
---
# <a name="deactivating-an-ndis-port"></a>停用 NDIS 端口





若要停用 NDIS 端口，微型端口驱动程序 (PnP) 事件向 NDIS 发送端口停用即插即用。 当微型端口驱动程序成功激活端口之后，驱动程序必须停用端口，然后才能释放端口。 另外，驱动程序可能会出于特定于应用程序的原因停用端口。 当端口停用后，可以重新激活它，但如果释放端口，则无法重新激活它。

若要发送端口停用 PnP 事件，小型端口驱动程序将使用 **NetEventPortDeactivation** PnP 事件代码来调用 [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) 函数。 若要停用端口，微型端口驱动程序必须将 **NdisMNetPnPEvent** 的 *NetPnPEvent* 参数指向的 [**NET \_ PNP \_ 事件 \_ 通知**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)结构的成员设置为，如下所示：

<a href="" id="portnumber"></a>**PortNumber**  
事件通知的源端口。 将此成员设置为零，因为 **NetPnPEvent** 成员指定的结构的 **Buffer** 成员中提供了端口号。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
描述端口停用事件的 [**NET \_ PNP \_ 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event) 结构。 设置此结构的成员，如下所示：

<a href="" id="netevent"></a>**NetEvent**  
描述事件的事件代码。 将此成员设置为 **NetEventPortDeactivation**。

<a href="" id="buffer"></a>**宽限**  
指向 NDIS \_ 端口号类型的元素的数组的指针 \_ 。 该数组包含微型端口驱动程序正在停用的所有端口的端口号。

<a href="" id="bufferlength"></a>**BufferLength**  
在 **缓冲区** 中指定的字节数。 将 **BufferLength** 设置为 **缓冲** 指向的数组的大小。 若要获取数组中的元素数，请将 **BufferLength** 中的值除以 NDIS \_ 端口 \_ 号数据类型的大小。

<a href="" id="other-members"></a>其他成员  
将 NET PNP 事件的其余成员设置 \_ \_ 为 **NULL**。

微型端口驱动程序可以为数组提供要停用的端口列表。 但是，如果微型端口适配器的默认端口是 **NetEventPortDeactivation** PnP 事件的目标，则默认端口必须是在数组中指定的唯一端口。

小型端口驱动程序可以随时停用活动端口。 但是，在微型端口驱动程序停用端口之前，必须确保没有未完成的状态指示或接收与该端口关联的指示。 微型端口驱动程序发送端口停用 PnP 事件之后，不能启动与停用的端口关联的任何状态或接收指示。

微型端口驱动程序还可以重新激活端口。 有关激活 NDIS 端口的详细信息，请参阅 [激活 Ndis 端口](activating-an-ndis-port.md)。

当微型端口驱动程序停用端口时，NDIS 会通知所有与 **NetEventPortDeactivation** PnP 事件绑定到微型端口驱动程序的协议驱动程序。 此 PnP 事件列出已更改为已分配状态且不包含已停用的任何端口的端口。 有关在协议驱动程序中处理端口停用事件的详细信息，请参阅 [处理端口停用 PnP 事件](handling-the-port-deactivation-pnp-event.md)。

在微型端口驱动程序分配 NDIS 端口之前，驱动程序必须调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，以便在 [**ndis \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes) 结构中设置注册属性。 小型端口驱动程序可以通过在 \_ 调用 NdisMSetMiniportAttributes 时设置 NDIS 微型端口 \_ 控件 \_ 默认 \_ 端口属性标志 **NdisMSetMiniportAttributes**，来控制默认端口的激活。 如果微型端口驱动程序假设有责任激活默认端口，而微型端口驱动程序激活了默认端口，则必须在从 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数返回之前停用默认端口。

由 NDIS 端口号元素数组指定的所有端口都 \_ \_ 必须处于 "已激活" 状态。 微型端口驱动程序不应尝试停用已停用的端口。

如果 NDIS 无法停用端口阵列中的任何端口，则端口阵列中的任何端口都不会更改状态。 如果由于某些指定的端口不存在而使停用失败， [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) 函数将返回 NDIS \_ 状态 " \_ \_ 端口返回值无效"。 如果由于某些端口未处于激活状态而导致停用失败， **NdisMNetPnPEvent** 将返回 NDIS 状态 " \_ \_ \_ 端口状态无效" \_ 返回值。

在对 **NdisMNetPnPEvent** 的调用返回之前，不会停用端口，并且微型端口驱动程序必须能够处理 OID 请求并发送与该端口关联的请求。

当微型端口驱动程序停用默认端口时，NDIS 会关闭过量协议驱动程序和微型端口适配器之间的所有绑定。 如果微型端口驱动程序尝试停用默认端口，并且已停用默认端口， [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) 将失败，并返回 NDIS \_ 状态 " \_ 端口状态无效" \_ \_ 返回值。 如果微型端口驱动程序尝试停用默认端口，并且默认端口不是在 NDIS 端口号元素数组中指定的唯一端口 \_ \_ ， **NdisMNetPnPEvent** 将失败，并返回 ndis 状态 " \_ \_ \_ 端口返回值无效"。 如果微型端口驱动程序将 **缓冲区** 成员设置为 **NULL** 或 **BufferLength** 成员设置为零，则 NDIS 将失败 **NdisMNetPnPEvent** 调用，并返回 ndis \_ 状态 " \_ \_ 参数返回值无效"。

成功停用端口后，端口将处于已分配状态。 小型端口驱动程序无法表示已接收的数据或端口状态。

 

