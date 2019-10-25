---
title: 添加和删除低功耗协议卸载
description: 添加和删除低功耗协议卸载
ms.assetid: f00f13b4-9204-4480-884a-407684a4b2d4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ea638ceb0b73dc26b5650ffd35925c50859104
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838246"
---
# <a name="adding-and-deleting-low-power-protocol-offloads"></a>添加和删除低功耗协议卸载





为了添加低功率协议卸载，NDIS 协议驱动程序会发出 oid\_PM 的 OID 集请求[\_添加\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

**请注意**  传入数据包是否与卸载的协议和模式匹配（例如，由于配置错误），网络适配器应响应数据包并唤醒计算机。

 

[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)结构包含以下信息：

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
<td align="left"><p><strong>大事</strong></p></td>
<td align="left"><p>包含协议卸载的优先级。 如果过量驱动程序在没有可用于更多协议卸载的资源时添加更高优先级的协议卸载，NDIS 可能会删除较低优先级的协议卸载以释放资源。 微型端口驱动程序应忽略此成员。 协议驱动程序可以提供从 NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_LOWEST 到 NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_HIGHEST 的预定义范围内的任何值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadType</strong></p></td>
<td align="left"><p>包含指定协议卸载类型的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)"><strong>NDIS_PM_PROTOCOL_OFFLOAD_TYPE</strong></a>值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>友好</strong></p></td>
<td align="left"><p>包含<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string" data-raw-source="[&lt;strong&gt;NDIS_PM_COUNTED_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_counted_string)"><strong>NDIS_PM_COUNTED_STRING</strong></a>结构，该结构包含用户可读的低功率协议卸载说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadId</strong></p></td>
<td align="left"><p>包含一个用于标识卸载协议的 NDIS 提供的值。 在 NDIS 将<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload" data-raw-source="[OID_PM_ADD_PROTOCOL_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)">OID_PM_ADD_PROTOCOL_OFFLOAD</a>的 OID 请求发送到基础 NDIS 驱动程序或完成对过量驱动程序的请求之前，ndis 会将<strong>ProtocolOffloadId</strong>设置为一个值，该值在协议卸载网络适配器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NextProtocolOffloadOffset</strong></p></td>
<td align="left"><p>包含<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list" data-raw-source="[OID_PM_PROTOCOL_OFFLOAD_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)">OID_PM_PROTOCOL_OFFLOAD_LIST</a> oid 列表中的下一个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)"><strong>NDIS_PM_PROTOCOL_OFFLOAD</strong></a>结构的偏移量，即 OID 请求<em>InformationBuffer</em>的起始位置。 有关 OID_PM_PROTOCOL_OFFLOAD_LIST 的详细信息，请参阅<a href="obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md" data-raw-source="[Obtaining the Current Parameter Settings of Low Power Protocol Offloads](obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md)">获取低功率协议卸载的当前参数设置</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadParameters</strong></p></td>
<td align="left"><p>包含联合中的一个<strong>IPv4ARPParameters</strong>、 <strong>IPv6NSParameters</strong>或<strong>Dot11RSNRekeyParameters</strong>结构。</p>
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
<td align="left"><p>包含 IPv6 邻居请求（NS）参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Dot11RSNRekeyParameters</p></td>
<td align="left"><p>包含 IEEE 802.11 稳健安全网络（RSN）握手参数</p></td>
</tr>
</tbody>
</table>
<p> </p></td>
</tr>
</tbody>
</table>

 

NDIS 为每个卸载的协议的网络适配器分配一个唯一的标识符。 协议卸载标识符是在网络适配器上卸载的每个协议的唯一值。 但是，协议卸载标识符在所有网络适配器之间不是全局唯一的。 当 NDIS 发送 Oid\_PM 时，NDIS 会将此标识符传递给基础微型端口驱动程序[\_将\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)OID 请求添加到微型端口驱动程序。 如果卸载协议成功，NDIS 会将标识符返回到卸载协议的过量驱动程序。 过量驱动程序使用标识符来删除以前卸载的协议。 在从网络适配器中删除卸载的协议时，也会在状态指示中对上层驱动程序使用协议卸载标识符。

协议驱动程序必须先从网络适配器中删除所有卸载的协议，然后才能关闭对该网络适配器的绑定。 为了消除低功率协议卸载，协议驱动程序会将 Oid\_PM 的 OID 集请求发送[\_删除\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-protocol-offload)。 [ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向协议卸载标识符的指针。

NDIS 允许多个 NDIS 协议驱动程序将协议卸载添加到同一个网络适配器。 为了确保在请求的卸载协议数高于网络适配器可支持的数目时，已将正确的一组协议卸载到网络适配器，协议驱动程序将优先级分配给每个卸载的协议。 当由于网络适配器资源不足而导致 NDIS 无法卸载新的高优先级协议时，NDIS 将删除低优先级的已卸载协议（如果有），并尝试再次卸载高优先级协议。

**请注意**  微型端口驱动程序应使低功耗协议卸载添加请求失败并返回状态\_NDIS\_PM\_协议\_卸载\_LIST\_完整状态代码，以允许 NDIS 重新设置优先级协议卸载。

 

由于卸载了高优先级的协议，因此删除了优先级较低的一个协议，NDIS 会将[**ndis\_状态\_PM 发送\_卸载\_拒绝**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-offload-rejected)的状态指示，通知过量驱动程序设置删除的协议卸载。 [**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含被拒绝的协议卸载的协议卸载标识符。 NDIS 在 Ndis\_PM 的**ProtocolOffloadId**成员中提供了协议卸载标识符[ **\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构。

 

 





