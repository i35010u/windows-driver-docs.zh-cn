---
title: 激活 NDIS 端口
description: 激活 NDIS 端口
ms.assetid: 0f3bfda2-8faa-4a92-a76b-0c0c361bd667
keywords:
- 端口 WDK NDIS，激活
- NDIS 端口 WDK，激活
- 激活 NDIS 端口
- 端口状态 WDK NDIS
- 激活即插即用事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69f6a88960f4de5b5d90052d8cf472a8017d04bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542192"
---
# <a name="activating-an-ndis-port"></a>激活 NDIS 端口





后微型端口驱动程序已成功分配的 NDIS 端口，并在 NDIS 函数中使用的端口号之前, 驱动程序必须激活该端口。 若要激活该端口，微型端口驱动程序将到 NDIS 发送端口激活插 (PnP) 事件。 若要将发送端口的激活即插即用事件，微型端口驱动程序，请使用**NetEventPortActivation** PnP 对的调用中的事件代码[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)函数。

若要激活端口，微型端口驱动程序必须设置的成员[ **NET\_PNP\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)结构的*NetPnPEvent*的参数**NdisMNetPnPEvent**指向，如下所示：

<a href="" id="portnumber"></a>**PortNumber**  
事件通知的源端口。 将此成员设置为零，因为在提供的端口号**缓冲区**结构中的成员的**NetPnPEvent**成员指定。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
一个[ **NET\_PNP\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff568751)描述端口激活事件的结构。 设置此结构的成员，如下所示：

<a href="" id="netevent"></a>**NetEvent**  
一个描述事件的事件代码。 将此成员设置为**NetEventPortActivation**。

<a href="" id="buffer"></a>**缓冲区**  
指向的链接列表的指针[ **NDIS\_端口**](https://msdn.microsoft.com/library/windows/hardware/ff566769)结构。 **下一步**成员的 NDIS\_端口结构指向下一步 NDIS\_端口列表中的结构。

<a href="" id="bufferlength"></a>**BufferLength**  
中指定的字节数**缓冲区**。 设置**BufferLength** NDIS 大小\_端口结构。

<a href="" id="other-members"></a>其他成员  
设置网络的其余成员\_PNP\_事件**NULL**。

微型端口驱动程序列出了已更改状态从非活动状态为活动的链接列表中的端口[ **NDIS\_端口**](https://msdn.microsoft.com/library/windows/hardware/ff566769)结构。 但是，如果微型端口适配器的默认端口为的目标**NetEventPortActivation**即插即用事件的默认端口必须是唯一的端口列表中。

当微型端口驱动程序通知 NDIS 端口的激活 （和可能是此通知之前调用返回） 时，微型端口驱动程序必须准备好处理发送请求和 OID 与端口相关联的请求。 微型端口驱动程序不能使用状态中的新激活端口的端口号或接收指示调用的后面[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)返回。

NDIS 默认端口处于活动状态后，不会通知有关直到激活端口基础驱动程序。 当调用 NDIS [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)协议驱动程序，NDIS 函数提供了一系列中的所有当前活动端口**ActivePorts** 的成员[**NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)结构*BindParameters*参数指向。 当微型端口驱动程序将激活新端口时，NDIS 通知绑定到的微型端口驱动程序使用的协议驱动程序的所有**NetEventPortActivation**即插即用事件。 有关处理协议驱动程序中的这些端口激活事件的详细信息，请参阅[处理端口激活即插即用事件](handling-the-port-activation-pnp-event.md)。

该驱动程序微型端口驱动程序分配的 NDIS 端口之前，必须调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)中的属性函数将设置注册[ **NDIS\_微型端口\_适配器\_注册\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构。 微型端口驱动程序可以通过设置 NDIS 控制默认端口的激活\_微型端口\_控件\_默认\_端口属性标志时它们调用**NdisMSetMiniportAttributes**. 如果微型端口驱动程序负责在激活默认端口，直到微型端口驱动程序激活默认端口与端口激活即插即用事件 NDIS 并不会启动微型端口适配器与基础驱动程序之间的绑定。

所有端口所指定的链接列表的 NDIS\_端口结构必须处于已分配状态。 微型端口驱动程序不应尝试激活已处于活动状态; 的端口如果该驱动程序会尝试激活活动端口，NDIS treates 作为端口激活失败的情况。

如果 NDIS 无法激活列表上的任何端口，就会失败的调用[ **NdisMNetPnPEvent**](https://msdn.microsoft.com/library/windows/hardware/ff563616)，并无列表上的端口将状态更改为已激活的状态。 如果无法激活端口，因为一些的端口不存在，NDIS **NdisMNetPnPEvent**返回 NDIS\_状态\_无效\_端口返回值。 如果无法激活端口，因为一些端口未处于已分配状态，NDIS **NdisMNetPnPEvent**返回 NDIS\_状态\_无效\_端口\_状态返回值.

已成功激活端口后，该端口将处于激活状态。 微型端口驱动程序可以指示接收到的数据，以及处于激活状态的端口的状态。

NDIS 将传递到的默认端口的身份验证状态[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)在正常**DefaultPortAuthStates**隶属[**NDIS\_微型端口\_INIT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565972)结构。 如果微型端口驱动程序控制的默认端口，当微型端口驱动程序激活默认端口时，它可以使用的默认身份验证设置来激活默认端口。 若要使用的默认身份验证设置，设置 NDIS\_端口\_CHAR\_使用\_默认\_身份验证\_中的设置标志**标志**的成员[ **NDIS\_端口\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566791)结构。 微型端口驱动程序可以使用 NDIS\_端口\_CHAR\_使用\_默认\_身份验证\_为它们分配和激活的端口设置标志。 对于激活的情况，NDIS 到新激活的端口分配默认身份验证状态，并忽略传递给身份验证状态[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)为**NetEventPortActivation**事件。

有关控制默认端口，然后在分配的端口的详细信息，请参阅[Allocating NDIS 端口](allocating-an-ndis-port.md)。

 

 





