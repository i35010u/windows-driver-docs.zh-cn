---
title: 添加和删除 LAN 唤醒模式
description: 添加和删除 LAN 唤醒模式
ms.assetid: 87e16ba6-0974-4921-b846-97d105e5dd30
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b3d7f8df00eb410bcf4f3b27e2eb5444cc38e7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838244"
---
# <a name="adding-and-deleting-wake-on-lan-patterns"></a>添加和删除 LAN 唤醒模式





为了添加 LAN 唤醒（WOL）模式，NDIS 协议驱动程序会发出 oid\_PM 的 OID 集请求[\_添加\_WOL\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的指针。 如果网络适配器支持 WOL 数据包，则协议驱动程序应指定 WOL 数据包。 如果网络适配器不支持 WOL 数据包，则协议驱动程序应使用 WOL 位图唤醒方法。

NDIS\_PM\_WOL\_模式包含以下信息：

<a href="" id="priority"></a>**大事**  
包含 WOL 模式的优先级。 如果过量驱动程序在没有可用于更多 WOL 模式的资源时添加更高优先级的 WOL 模式，NDIS 可能会删除较低优先级的 WOL 模式以释放资源。 微型端口驱动程序应忽略此成员。 协议驱动程序可以指定从 NDIS\_PM 中的预定义范围内的任何优先级\_WOL\_优先级\_最低到 NDIS\_\_\_\_最高优先级。

<a href="" id="wolpackettype"></a>**WoLPacketType**  
包含一个[**NDIS\_PM\_wol\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_wol_packet)枚举值，该枚举值指定 wol 数据包的类型。

<a href="" id="friendlyname"></a>**友好**  
包含[**NDIS\_PM\_计数\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string)结构，其中包含对 WOL 数据包的用户可读说明。

<a href="" id="patternid"></a>**PatternId**  
包含一个用于标识 WOL 模式的 NDIS 提供的值。 在 NDIS [\_PM 发送 OID 之前\_将\_WOL\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)OID 请求向下添加到基础 NDIS 驱动程序或完成对过量驱动程序的请求，NDIS 会将**PatternId**设置为在网络适配器上的 WOL 模式中唯一的值。

<a href="" id="nextwolpatternoffset"></a>**NextWoLPatternOffset**  
包含从一个[**ndis\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构到下一个 ndis\_PM 之间的偏移量（从 OID 请求**InformationBuffer**的开始） wol 模式结构到下一个 ndis pm [\_wol\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-wol-pattern-list)\_\_\_\_ 有关 OID 的详细信息\_PM\_WOL\_模式\_列表，请参阅[获取 Wol 模式的当前设置](obtaining-the-current-settings-of-wol-patterns.md)。

<a href="" id="wolpattern"></a>**WoLPattern**  
包含联合中的**IPv4TcpSynParameters**、 **IPv6TcpSynParameters**、 **EapolRequestIdMessageParameters**或**WoLBitMapPattern**结构之一。

<a href="" id="ipv4tcpsynparameters"></a>**IPv4TcpSynParameters**  
包含 IPv4 TCP 同步（SYN）信息。

<a href="" id="ipv6tcpsynparameters"></a>**IPv6TcpSynParameters**  
包含 IPv6 TCP SYN 信息。

<a href="" id="eapolrequestidmessageparameters"></a>**EapolRequestIdMessageParameters**  
包含 802.1 X EAP over LAN （EAPOL）请求标识消息参数。

<a href="" id="wolbitmappattern"></a>**WoLBitMapPattern**  
包含 WOL 位图模式规范。

NDIS 为每个 WOL 模式的网络适配器分配一个唯一的标识符。 模式标识符是网络适配器上设置的每个模式的唯一值。 但是，所有网络适配器的模式标识符不是全局唯一的。 当 NDIS 发送 OID\_PM 时，NDIS 会将标识符传递给基础网络适配器[\_将\_WOL\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)OID 请求添加到微型端口驱动程序。 如果添加 WOL 模式成功，NDIS 会将标识符返回到已添加 WOL 模式的过量驱动程序。 过量驱动程序使用标识符来删除以前添加的 WOL 模式。 在从网络适配器中删除 WOL 模式时，还会将模式标识符用于向过量驱动程序的状态指示。

协议驱动程序必须发出 Oid\_PM 的 OID 集请求[\_删除\_WOL\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-wol-pattern)，以便在关闭到网络适配器的绑定之前删除其添加到网络适配器的所有模式。 [ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向模式标识符的指针。

用户模式应用程序使用 GUID\_PM\_删除\_WOL\_模式 WMI GUID，从网络适配器中删除以前添加的 WOL 模式。 NDIS 将此 WMI 请求转换为 Oid\_PM 的 OID 集请求\_删除网络适配器的[\_WOL\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-wol-pattern)。 当应用程序停止网络适配器之前，NDIS 会删除该应用程序添加的所有 WOL 模式。

NDIS 允许多个 NDIS 协议驱动程序将 WOL 模式添加到同一个网络适配器。 若要确保在请求的 WOL 模式数量高于网络适配器可支持的数量时设置正确的 WOL 模式集，协议驱动程序会在 NDIS\_PM\_WOL\_模式结构的**优先级**成员中为每个请求的 wol 模式分配优先级。 当 NDIS 因为网络适配器不在资源外而无法添加新的高优先级 WOL 模式时，NDIS 将删除较低优先级模式（如果有），并再次尝试添加高优先级模式。

**请注意**  微型端口驱动程序应使模式添加请求失败并返回状态\_NDIS\_PM\_WOL\_模式\_列出\_完整状态代码，以允许 NDIS 重新确定模式的优先级。

 

如果 NDIS 删除一个较低优先级模式，它会通知过量驱动程序，将已删除的模式设置为[**NDIS\_状态\_PM\_WOL\_模式\_拒绝**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)的状态指示。 [**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含被拒绝的 wol 模式的 WOL 模式标识符的 ULONG。 NDIS 在[**ndis\_PM\_wol\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的**PatternId**成员中提供了 wol 模式标识符。

对于可能使用基础结构元素在整个基础结构中漫游的模式时，可以使用基础结构元素来卸载模式的无线网络适配器，新基础结构元素可能不支持相同的功能，微型端口驱动程序可以将[**NDIS\_状态\_\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)

 

 





