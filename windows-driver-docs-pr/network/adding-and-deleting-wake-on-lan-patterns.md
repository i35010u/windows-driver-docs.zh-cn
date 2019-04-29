---
title: 添加和删除 LAN 唤醒模式
description: 添加和删除 LAN 唤醒模式
ms.assetid: 87e16ba6-0974-4921-b846-97d105e5dd30
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee69a94fce480a52fe0538dc37cf6ff9b0d13479
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367765"
---
# <a name="adding-and-deleting-wake-on-lan-patterns"></a>添加和删除 LAN 唤醒模式





若要添加的 LAN 唤醒 (WOL) 模式，协议的 NDIS 驱动程序发出的 OID 集请求[OID\_PM\_添加\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569764)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)结构。 如果该 WOL 数据包支持的网络适配器，协议驱动程序应指定 WOL 数据包。 网络适配器不支持的 WOL 数据包，协议驱动程序应使用 WOL 位图唤醒方法。

NDIS\_PM\_WOL\_模式包括以下信息：

<a href="" id="priority"></a>**优先级**  
包含 WOL 模式的优先级。 如果基础驱动程序添加更高的优先级 WOL 模式，当没有资源可用于更多的 WOL 模式，NDIS 可能会删除较低的优先级 WOL 模式来释放资源。 微型端口驱动程序应忽略此成员。 协议驱动程序可以指定从 NDIS 预定义的范围内任何优先级\_PM\_WOL\_优先级\_到 NDIS 最低\_PM\_WOL\_优先级\_最高。

<a href="" id="wolpackettype"></a>**WoLPacketType**  
包含[ **NDIS\_PM\_WOL\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff566766)枚举值，指定的 WOL 数据包类型。

<a href="" id="friendlyname"></a>**FriendlyName**  
包含[ **NDIS\_PM\_盘点\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff566753)结构，其中包含的 WOL 数据包的用户可读说明。

<a href="" id="patternid"></a>**PatternId**  
包含用于标识 WOL 模式的 NDIS 提供值。 NDIS 发送之前[OID\_PM\_添加\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569764)OID 请求到的基础的 NDIS 驱动程序或完成对基础驱动程序的请求，NDIS 设置**PatternId**为在网络适配器上的 WOL 模式是唯一的值。

<a href="" id="nextwolpatternoffset"></a>**NextWoLPatternOffset**  
包含的偏移量 (从 OID 请求开头**InformationBuffer**) 之一[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)结构与下一步 NDIS\_PM\_WOL\_列表中的模式结构[OID\_PM\_WOL\_模式\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569772)OID。 有关 OID 的详细信息\_PM\_WOL\_模式\_列表中，请参阅[获取 WOL 模式当前设置](obtaining-the-current-settings-of-wol-patterns.md)。

<a href="" id="wolpattern"></a>**WoLPattern**  
包含之一**IPv4TcpSynParameters**， **IPv6TcpSynParameters**， **EapolRequestIdMessageParameters**，或**WoLBitMapPattern**联合中的结构。

<a href="" id="ipv4tcpsynparameters"></a>**IPv4TcpSynParameters**  
包含 IPv4 TCP 同步 (SYN) 的信息。

<a href="" id="ipv6tcpsynparameters"></a>**IPv6TcpSynParameters**  
包含 IPv6 TCP SYN 的信息。

<a href="" id="eapolrequestidmessageparameters"></a>**EapolRequestIdMessageParameters**  
通过 LAN (EAPOL) 请求标识消息参数包含 802.1 X EAP。

<a href="" id="wolbitmappattern"></a>**WoLBitMapPattern**  
包含 WOL 位图模式规范。

NDIS 将分配唯一的网络适配器添加到每个 WOL 模式的标识符。 模式标识符是为每个网络适配器设置的模式的唯一值。 但是，模式标识符不是全局唯一跨所有网络适配器。 NDIS 将标识符传递到基础的网络适配器时 NDIS 发送[OID\_PM\_添加\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569764)OID 请求到微型端口驱动程序。 如果成功添加 WOL 模式，NDIS 返回添加的 WOL 模式的基础驱动程序的标识符。 基础驱动程序使用标识符来删除以前添加的 WOL 模式。 模式标识符还可在对基础驱动程序的状态指示时 WOL 模式已从网络适配器。

协议驱动程序必须发出的 OID 集请求[OID\_PM\_删除\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569771)中删除所有他们关闭之前添加到的网络适配器的模式绑定到该网络适配器。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向模式标识符。

用户模式应用程序使用的 GUID\_PM\_删除\_WOL\_模式 WMI GUID，以便从网络适配器中删除以前添加的 WOL 模式。 NDIS 转换对 OID 集请求的 WMI 请求[OID\_PM\_删除\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569771)的网络适配器。 NDIS 将删除所有之前停止的网络适配器，从网络适配器添加应用程序的 WOL 模式。

NDIS 允许多个 NDIS 协议驱动程序将 WOL 模式添加到相同的网络适配器。 若要确保一组合适的 WOL 模式已设置的数量的请求的 WOL 模式比网络适配器可以支持更高版本时，协议驱动程序分配优先级中每个请求 WOL 模式**优先级**成员的 NDIS\_PM\_WOL\_模式结构。 当 NDIS 无法添加新的高优先级 WOL 模式，因为网络适配器的资源不足时，NDIS 删除一个较低的优先级模式 （如果有），并尝试再次添加高优先级模式。

**请注意**  微型端口驱动程序应失败模式添加请求，并返回状态\_NDIS\_PM\_WOL\_模式\_列表\_到完整的状态代码允许 NDIS 重新进行优先级排序模式。

 

如果 NDIS 删除较低的优先级模式之一，它将通知设置已删除的模式与基础驱动程序[ **NDIS\_状态\_PM\_WOL\_模式\_REJECTED** ](https://msdn.microsoft.com/library/windows/hardware/ff567414)状态指示。 **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含的 WOL 模式标识符的 ULONG拒绝 WOL 模式。 NDIS 提供中的 WOL 模式标识符**PatternId**的成员[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)结构。

对于无线网络适配器的可能使用的基础结构元素来减轻负载模式，因为它在基础结构之间漫游，新的基础结构元素可能不支持相同的功能和微型端口驱动程序可以发送[ **NDIS\_状态\_PM\_WOL\_模式\_已拒绝**](https://msdn.microsoft.com/library/windows/hardware/ff567414)状态指示与相应的状态代码。

 

 





