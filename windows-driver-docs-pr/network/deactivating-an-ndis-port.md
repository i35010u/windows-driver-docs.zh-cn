---
title: 停用 NDIS 端口
description: 停用 NDIS 端口
ms.assetid: 2a5d288f-b6ea-4b63-91a3-44155aae8064
keywords:
- 端口 WDK NDIS，停用
- NDIS 端口 WDK，停用
- 停用 NDIS 端口 WDK NDIS
- 停用 PnP 事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73c0df73910ad0432900f31f45acc0019320a313
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834956"
---
# <a name="deactivating-an-ndis-port"></a>停用 NDIS 端口





若要停用 NDIS 端口，小型端口驱动程序会将端口停用即插即用（PnP）事件发送到 NDIS。 当微型端口驱动程序成功激活端口之后，驱动程序必须停用端口，然后才能释放端口。 另外，驱动程序可能会出于特定于应用程序的原因停用端口。 当端口停用后，可以重新激活它，但如果释放端口，则无法重新激活它。

若要发送端口停用 PnP 事件，小型端口驱动程序将使用**NetEventPortDeactivation** PnP 事件代码来调用[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)函数。 若要停用端口，微型端口驱动程序必须将[**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)的成员设置为**NdisMNetPnPEvent**的*NETPNPEVENT*参数指向的\_通知结构，如下所示：

<a href="" id="portnumber"></a>**PortNumber**  
事件通知的源端口。 将此成员设置为零，因为**NetPnPEvent**成员指定的结构的**Buffer**成员中提供了端口号。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
用于描述端口停用事件的[**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)结构。 设置此结构的成员，如下所示：

<a href="" id="netevent"></a>**NetEvent**  
描述事件的事件代码。 将此成员设置为**NetEventPortDeactivation**。

<a href="" id="buffer"></a>**宽限**  
指向 NDIS\_端口的数组的指针\_数值类型的元素。 该数组包含微型端口驱动程序正在停用的所有端口的端口号。

<a href="" id="bufferlength"></a>**BufferLength**  
在**缓冲区**中指定的字节数。 将**BufferLength**设置为**缓冲**指向的数组的大小。 若要获取数组中的元素数，请将**BufferLength**中的值除以 NDIS\_端口\_number 数据类型的大小。

<a href="" id="other-members"></a>其他成员  
将 NET\_PNP\_事件的剩余成员设置为**NULL**。

微型端口驱动程序可以为数组提供要停用的端口列表。 但是，如果微型端口适配器的默认端口是**NetEventPortDeactivation** PnP 事件的目标，则默认端口必须是在数组中指定的唯一端口。

小型端口驱动程序可以随时停用活动端口。 但是，在微型端口驱动程序停用端口之前，必须确保没有未完成的状态指示或接收与该端口关联的指示。 微型端口驱动程序发送端口停用 PnP 事件之后，不能启动与停用的端口关联的任何状态或接收指示。

微型端口驱动程序还可以重新激活端口。 有关激活 NDIS 端口的详细信息，请参阅[激活 Ndis 端口](activating-an-ndis-port.md)。

当微型端口驱动程序停用端口时，NDIS 会通知所有与**NetEventPortDeactivation** PnP 事件绑定到微型端口驱动程序的协议驱动程序。 此 PnP 事件列出已更改为已分配状态且不包含已停用的任何端口的端口。 有关在协议驱动程序中处理端口停用事件的详细信息，请参阅[处理端口停用 PnP 事件](handling-the-port-deactivation-pnp-event.md)。

在微型端口驱动程序分配 NDIS 端口之前，驱动程序必须调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，以便在[**NDIS\_微型端口\_适配器\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)中设置注册属性构造. 小型端口驱动程序可以通过在调用**NdisMSetMiniportAttributes**时将 NDIS\_微型端口\_控件\_默认\_端口属性标志，来控制默认端口的激活。 如果微型端口驱动程序假设有责任激活默认端口，而微型端口驱动程序激活了默认端口，则必须在从[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数返回之前停用默认端口。

由\_NDIS 数组指定的所有端口\_NUMBER 元素都必须处于 "已激活" 状态。 微型端口驱动程序不应尝试停用已停用的端口。

如果 NDIS 无法停用端口阵列中的任何端口，则端口阵列中的任何端口都不会更改状态。 如果由于某些指定端口不存在而使停用失败， [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)函数将返回 NDIS\_状态\_无效的\_端口返回值。 如果由于某些端口未处于 "已激活" 状态而导致停用失败， **NdisMNetPnPEvent**将返回 NDIS\_状态\_无效\_端口\_状态返回值。

在对**NdisMNetPnPEvent**的调用返回之前，不会停用端口，并且微型端口驱动程序必须能够处理 OID 请求并发送与该端口关联的请求。

当微型端口驱动程序停用默认端口时，NDIS 会关闭过量协议驱动程序和微型端口适配器之间的所有绑定。 如果微型端口驱动程序尝试停用默认端口，并且已停用默认端口， [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)将失败，并返回 NDIS\_状态\_无效\_端口\_状态返回值。 如果微型端口驱动程序尝试停用默认端口，并且默认端口不是在 NDIS\_端口\_号元素的数组中指定的唯一端口， **NdisMNetPnPEvent**将失败并返回 NDIS\_状态\_\_端口返回值无效。 如果微型端口驱动程序将**缓冲区**成员设置为**NULL**或**BufferLength**成员设置为零，则 ndis 将失败**NdisMNetPnPEvent**调用并返回 ndis\_状态\_无效\_参数返回值。

成功停用端口后，端口将处于已分配状态。 小型端口驱动程序无法表示已接收的数据或端口状态。

 

 





