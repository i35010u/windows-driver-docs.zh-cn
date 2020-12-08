---
title: 添加和删除低功耗协议卸载
description: 添加和删除低功耗协议卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c03448760905e7215abe5a68b37247a1d1f495c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826997"
---
# <a name="adding-and-deleting-low-power-protocol-offloads"></a>添加和删除低功耗协议卸载





若要添加低功率协议卸载，NDIS 协议驱动程序会发出 oid [ \_ PM \_ 添加 \_ 协议 \_ 卸载](./oid-pm-add-protocol-offload.md)的 oid 设置请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

**注意**  如果传入数据包与被卸载的协议和模式相匹配 (例如，由于配置错误) ，网络适配器应响应数据包并唤醒计算机。

 

[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)结构包含以下信息：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Priority</strong></p></td>
<td align="left"><p>包含协议卸载的优先级。 如果过量驱动程序在没有可用于更多协议卸载的资源时添加更高优先级的协议卸载，NDIS 可能会删除较低优先级的协议卸载以释放资源。 微型端口驱动程序应忽略此成员。 协议驱动程序可提供从 NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_LOWEST 到 NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_HIGHEST 的预定义范围内的任何值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadType</strong></p></td>
<td align="left"><p>包含指定协议卸载类型的 <a href="/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD_TYPE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)"><strong>NDIS_PM_PROTOCOL_OFFLOAD_TYPE</strong></a> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FriendlyName</strong></p></td>
<td align="left"><p>包含一个 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string" data-raw-source="[&lt;strong&gt;NDIS_PM_COUNTED_STRING&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string)"><strong>NDIS_PM_COUNTED_STRING</strong></a> 结构，它包含用户可读的低功率协议卸载说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadId</strong></p></td>
<td align="left"><p>包含一个用于标识卸载协议的 NDIS 提供的值。 在 NDIS 将 <a href="/windows-hardware/drivers/network/oid-pm-add-protocol-offload" data-raw-source="[OID_PM_ADD_PROTOCOL_OFFLOAD](./oid-pm-add-protocol-offload.md)">OID_PM_ADD_PROTOCOL_OFFLOAD</a> 的 OID 请求发送到基础 NDIS 驱动程序或完成对过量驱动程序的请求之前，ndis 会将 <strong>ProtocolOffloadId</strong> 设置为在网络适配器上的协议卸载之间唯一的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NextProtocolOffloadOffset</strong></p></td>
<td align="left"><p>包含<em>InformationBuffer</em>oid <a href="/windows-hardware/drivers/network/oid-pm-protocol-offload-list" data-raw-source="[OID_PM_PROTOCOL_OFFLOAD_LIST](./oid-pm-protocol-offload-list.md)">OID_PM_PROTOCOL_OFFLOAD_LIST</a>列表中的下一个<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)"><strong>NDIS_PM_PROTOCOL_OFFLOAD</strong></a>结构的偏移量，即 oid 请求的起始位置。 有关 OID_PM_PROTOCOL_OFFLOAD_LIST 的详细信息，请参阅 <a href="obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md" data-raw-source="[Obtaining the Current Parameter Settings of Low Power Protocol Offloads](obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md)">获取低功率协议卸载的当前参数设置</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadParameters</strong></p></td>
<td align="left"><p>包含联合中的一个 <strong>IPv4ARPParameters</strong>、 <strong>IPv6NSParameters</strong>或 <strong>Dot11RSNRekeyParameters</strong> 结构。</p>
<p></p>
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IPv4ARPParameters</p></td>
<td align="left"><p>包含 IPv4 ARP 参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IPv6NSParameters</p></td>
<td align="left"><p>包含 (NS) 参数的 IPv6 邻居请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Dot11RSNRekeyParameters</p></td>
<td align="left"><p>包含 IEEE 802.11 稳健安全网络 (RSN) 握手参数</p></td>
</tr>
</tbody>
</table>
<p> </p></td>
</tr>
</tbody>
</table>

 

NDIS 为每个卸载的协议的网络适配器分配一个唯一的标识符。 协议卸载标识符是在网络适配器上卸载的每个协议的唯一值。 但是，协议卸载标识符在所有网络适配器之间不是全局唯一的。 当 NDIS 将 [oid \_ PM \_ 添加 \_ \_ ](./oid-pm-add-protocol-offload.md) 到小型微端口驱动程序时，ndis 会将此标识符传递给基础微型端口驱动程序。 如果卸载协议成功，NDIS 会将标识符返回到卸载协议的过量驱动程序。 过量驱动程序使用标识符来删除以前卸载的协议。 在从网络适配器中删除卸载的协议时，也会在状态指示中对上层驱动程序使用协议卸载标识符。

协议驱动程序必须先从网络适配器中删除所有卸载的协议，然后才能关闭对该网络适配器的绑定。 若要删除低功率协议卸载，协议驱动程序将发送 oid 的 OID 集请求，即 [ \_ \_ 删除 \_ 协议 \_ 卸载](./oid-pm-remove-protocol-offload.md)。 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向协议卸载标识符的指针。

NDIS 允许多个 NDIS 协议驱动程序将协议卸载添加到同一个网络适配器。 为了确保在请求的卸载协议数高于网络适配器可支持的数目时，已将正确的一组协议卸载到网络适配器，协议驱动程序将优先级分配给每个卸载的协议。 如果由于网络适配器资源不足而导致 NDIS 无法卸载新的高优先级协议，NDIS 将删除低优先级卸载协议中的一个 (如果任何) 并尝试再次卸载高优先级协议。

**注意**  微型端口驱动程序应使低功率协议卸载添加请求失败，并返回状态 \_ NDIS \_ PM \_ 协议 \_ 卸载 \_ 列表 \_ 完整状态代码，以允许 NDIS 重新设置协议卸载的优先级。

 

由于卸载了高优先级的协议，因此删除了一个优先级较低的已卸载协议，NDIS 发送了 [**ndis \_ 状态 \_ PM 卸载已 \_ \_ 拒绝**](./ndis-status-pm-offload-rejected.md) 的状态指示，通知设置已删除协议卸载的过量驱动程序。 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含被拒绝的协议卸载的协议卸载标识符。 NDIS 在 [**ndis \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的 **ProtocolOffloadId** 成员中提供了协议卸载标识符。

