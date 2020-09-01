---
title: 添加和删除 LAN 唤醒模式
description: 添加和删除 LAN 唤醒模式
ms.assetid: 87e16ba6-0974-4921-b846-97d105e5dd30
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a638fff29428cddf6a17132dfbbc315d037a9e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218175"
---
# <a name="adding-and-deleting-wake-on-lan-patterns"></a>添加和删除 LAN 唤醒模式





若要添加 LAN 唤醒 (WOL) 模式，NDIS 协议驱动程序会发出 oid 的 OID 集请求， [并 \_ \_ 添加 \_ WOL \_ 模式](./oid-pm-add-wol-pattern.md)。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ PM \_ WOL \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的指针。 如果网络适配器支持 WOL 数据包，则协议驱动程序应指定 WOL 数据包。 如果网络适配器不支持 WOL 数据包，则协议驱动程序应使用 WOL 位图唤醒方法。

NDIS \_ PM \_ WOL \_ 模式包含以下信息：

<a href="" id="priority"></a>**大事**  
包含 WOL 模式的优先级。 如果过量驱动程序在没有可用于更多 WOL 模式的资源时添加更高优先级的 WOL 模式，NDIS 可能会删除较低优先级的 WOL 模式以释放资源。 微型端口驱动程序应忽略此成员。 协议驱动程序可以指定预定义范围内的任何优先级，范围为从 \_ \_ \_ \_ 最低到 ndis \_ pm \_ wol \_ 优先级的 \_ 最高优先级。

<a href="" id="wolpackettype"></a>**WoLPacketType**  
包含一个用于指定 WOL 数据包类型的 [**NDIS \_ PM \_ WOL \_ 数据包**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_wol_packet) 枚举值。

<a href="" id="friendlyname"></a>**友好**  
包含一个 [**NDIS \_ PM \_ 计数 \_ 字符串**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string) 结构，其中包含对 WOL 数据包的用户可读说明。

<a href="" id="patternid"></a>**PatternId**  
包含一个用于标识 WOL 模式的 NDIS 提供的值。 在 NDIS 发送 OID PM 之前，请向下 [ \_ \_ 添加 \_ WOL \_ 模式](./oid-pm-add-wol-pattern.md) OID 请求，或完成对过量驱动程序的请求，NDIS 会将 **PATTERNID** 设置为网络适配器上的 WOL 模式中唯一的值。

<a href="" id="nextwolpatternoffset"></a>**NextWoLPatternOffset**  
包含在 oid pm wol 模式**InformationBuffer** [** \_ \_ \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern) \_ \_ \_ [ \_ \_ \_ \_ 列表](./oid-pm-wol-pattern-list.md)oid 列表中，从 oid 请求 InformationBuffer) 的偏移量 (从一个 ndis pm wol 模式结构开始到下一个 ndis pm wol 模式结构的偏移量。 有关 OID \_ PM \_ wol 模式列表的详细信息 \_ \_ ，请参阅 [获取 WOL 模式的当前设置](obtaining-the-current-settings-of-wol-patterns.md)。

<a href="" id="wolpattern"></a>**WoLPattern**  
包含联合中的 **IPv4TcpSynParameters**、 **IPv6TcpSynParameters**、 **EapolRequestIdMessageParameters**或 **WoLBitMapPattern** 结构之一。

<a href="" id="ipv4tcpsynparameters"></a>**IPv4TcpSynParameters**  
包含 IPv4 TCP 同步 (SYN) 信息。

<a href="" id="ipv6tcpsynparameters"></a>**IPv6TcpSynParameters**  
包含 IPv6 TCP SYN 信息。

<a href="" id="eapolrequestidmessageparameters"></a>**EapolRequestIdMessageParameters**  
包含 802.1 X EAP over LAN (EAPOL) 请求标识消息参数。

<a href="" id="wolbitmappattern"></a>**WoLBitMapPattern**  
包含 WOL 位图模式规范。

NDIS 为每个 WOL 模式的网络适配器分配一个唯一的标识符。 模式标识符是网络适配器上设置的每个模式的唯一值。 但是，所有网络适配器的模式标识符不是全局唯一的。 当 NDIS 发送 OID PM 时，NDIS 会将标识符传递到基础网络适配器， [ \_ \_ 将 \_ WOL \_ 模式](./oid-pm-add-wol-pattern.md) OID 请求添加到微型端口驱动程序。 如果添加 WOL 模式成功，NDIS 会将标识符返回到已添加 WOL 模式的过量驱动程序。 过量驱动程序使用标识符来删除以前添加的 WOL 模式。 在从网络适配器中删除 WOL 模式时，还会将模式标识符用于向过量驱动程序的状态指示。

协议驱动程序必须发出 oid PM 的 OID 集请求， [ \_ \_ 删除 \_ WOL \_ 模式](./oid-pm-remove-wol-pattern.md) ，删除它们添加到网络适配器的所有模式，然后再关闭到该网络适配器的绑定。 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向模式标识符的指针。

用户模式应用程序使用 GUID \_ PM \_ 删除 \_ WOL \_ 模式 WMI GUID，从网络适配器中删除以前添加的 wol 模式。 NDIS 将此 WMI 请求转换为 Oid 的 OID 集请求，为网络适配器 [ \_ \_ 删除 \_ WOL \_ 模式](./oid-pm-remove-wol-pattern.md) 。 当应用程序停止网络适配器之前，NDIS 会删除该应用程序添加的所有 WOL 模式。

NDIS 允许多个 NDIS 协议驱动程序将 WOL 模式添加到同一个网络适配器。 为了确保在请求的 WOL 模式数量高于网络适配器可支持的数量时设置正确的 WOL 模式集，协议驱动程序会在 NDIS **Priority** \_ PM \_ WOL 模式结构的优先级成员中为每个请求的 wol 模式分配一个优先级 \_ 。 当 NDIS 因为网络适配器不在资源外而无法添加新的高优先级 WOL 模式时，NDIS 会删除较低优先级模式之一 (如果任何) 并再次尝试添加高优先级模式。

**注意**   小型端口驱动程序应使模式添加请求失败并返回状态 \_ NDIS \_ PM \_ WOL \_ 模式 \_ 列表 \_ 完整状态代码，以允许 NDIS 对模式重新设置优先级。

 

如果 NDIS 删除一个较低优先级模式，则会通知过量驱动程序，将已删除的模式设置为 [**NDIS \_ 状态 \_ PM \_ WOL \_ 模式 \_ 拒绝**](./ndis-status-pm-wol-pattern-rejected.md) 状态指示。 对于已拒绝的 WOL 模式， [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含 ULONG 模式标识符。 NDIS 在[**ndis \_ PM \_ WOL \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的**PatternId**成员中提供了 WOL 模式标识符。

对于可能使用基础结构元素在整个基础结构中漫游的模式时的无线网络适配器，新基础结构元素可能不支持相同的功能，微型端口驱动程序可以使用适当的状态代码发送 [**NDIS \_ 状态 \_ PM \_ WOL \_ 模式 \_ 拒绝**](./ndis-status-pm-wol-pattern-rejected.md) 状态指示。

 

