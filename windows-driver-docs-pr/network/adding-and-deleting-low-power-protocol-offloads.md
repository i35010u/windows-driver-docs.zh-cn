---
title: 添加和删除低功耗协议卸载
description: 添加和删除低功耗协议卸载
ms.assetid: f00f13b4-9204-4480-884a-407684a4b2d4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6ee07ef24464e7f9394f492e1e10b59eba11f46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383725"
---
# <a name="adding-and-deleting-low-power-protocol-offloads"></a>添加和删除低功耗协议卸载





若要添加低能耗协议卸载，协议的 NDIS 驱动程序发出的 OID 集请求[OID\_PM\_添加\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构。

**请注意**  的传入数据包与卸载的协议和模式匹配 （例如，由于配置错误），如果网络适配器应响应数据包并唤醒计算机。

 

[ **NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)结构包括以下信息：

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
<td align="left"><p><strong>优先级</strong></p></td>
<td align="left"><p>包含协议卸载的优先级。 如果过量驱动程序会添加更高的优先级协议卸载当没有资源可用于多个协议卸载、 NDIS 可能会删除较低的优先级协议卸载来释放资源。 微型端口驱动程序应忽略此成员。 协议驱动程序可以向 NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_HIGHEST 从 NDIS_PM_PROTOCOL_OFFLOAD_PRIORITY_LOWEST 提供预定义的范围内的任何值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadType</strong></p></td>
<td align="left"><p>包含<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_pm_protocol_offload_type)"> <strong>NDIS_PM_PROTOCOL_OFFLOAD_TYPE</strong> </a>值，该值指定的协议类型卸载。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FriendlyName</strong></p></td>
<td align="left"><p>包含<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_counted_string" data-raw-source="[&lt;strong&gt;NDIS_PM_COUNTED_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_counted_string)"> <strong>NDIS_PM_COUNTED_STRING</strong> </a>结构，其中包含用户可读的低能耗协议的说明卸载。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadId</strong></p></td>
<td align="left"><p>包含用于标识已卸载的协议的 NDIS 提供值。 NDIS 发送的 OID 请求之前<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload" data-raw-source="[OID_PM_ADD_PROTOCOL_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)">OID_PM_ADD_PROTOCOL_OFFLOAD</a>基础的 NDIS 驱动程序向下或在完成对基础驱动程序，NDIS 集请求<strong>ProtocolOffloadId</strong>为值唯一的而协议将卸载网络适配器上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NextProtocolOffloadOffset</strong></p></td>
<td align="left"><p>包含偏移量的 OID 请求开头<em>InformationBuffer</em>，到下一步<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload" data-raw-source="[&lt;strong&gt;NDIS_PM_PROTOCOL_OFFLOAD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)"> <strong>NDIS_PM_PROTOCOL_OFFLOAD</strong> </a>列表中的结构<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list" data-raw-source="[OID_PM_PROTOCOL_OFFLOAD_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)">OID_PM_PROTOCOL_OFFLOAD_LIST</a> OID。 有关 OID_PM_PROTOCOL_OFFLOAD_LIST 详细信息，请参阅<a href="obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md" data-raw-source="[Obtaining the Current Parameter Settings of Low Power Protocol Offloads](obtaining-the-current-parameter-settings-of-low-power-protocol-offload.md)">获取当前参数设置的低电源协议将卸载</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ProtocolOffloadParameters</strong></p></td>
<td align="left"><p>包含之一<strong>IPv4ARPParameters</strong>， <strong>IPv6NSParameters</strong>，或<strong>Dot11RSNRekeyParameters</strong>联合中的结构。</p>
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
<td align="left"><p>包含 IPv6 邻居招标 (NS) 参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Dot11RSNRekeyParameters</p></td>
<td align="left"><p>包含 IEEE 802.11 可靠安全的网络 (RSN) 握手参数</p></td>
</tr>
</tbody>
</table>
<p> </p></td>
</tr>
</tbody>
</table>

 

NDIS 分配对每个已卸载协议的网络适配器都是唯一的标识符。 协议卸载标识符是为每个网络适配器卸载的协议的唯一值。 但是，协议卸载标识符不是全局唯一跨所有网络适配器。 NDIS 在时 NDIS 发送到基础微型端口驱动程序将此标识符[OID\_PM\_添加\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)OID 请求到微型端口驱动程序。 如果卸载协议成功，NDIS 卸载协议的基础驱动程序返回的标识符。 基础驱动程序使用标识符来删除以前已卸载的协议。 协议卸载标识符还可在上层驱动程序的状态指示已卸载的协议从网络适配器中删除时。

协议驱动程序必须删除所有已卸载协议从网络适配器绑定到该网络适配器在关闭之前。 若要删除低能耗协议卸载，协议驱动程序发送的 OID 集请求[OID\_PM\_删除\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-remove-protocol-offload)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含协议卸载标识符的指针。

NDIS 允许多个 NDIS 协议驱动程序添加协议卸载到同一个网络适配器。 若要确保数请求卸载协议时，已被正确的协议集转移到的网络适配器是比网络适配器可以支持更高版本，协议驱动程序将优先级分配给每个已卸载协议。 当 NDIS 无法卸载新的高优先级协议，因为网络适配器的资源不足时、 NDIS 删除较低的优先级卸载协议之一 （如果有），并尝试再次卸载高优先级协议。

**请注意**  微型端口驱动程序应失败低能耗协议卸载添加请求并返回状态\_NDIS\_PM\_协议\_卸载\_列表\_完整状态代码，以允许 NDIS 重新进行优先级排序协议将卸载。

 

如果因此的卸载高优先级协议，一个较低优先级的卸载协议删除时，将发送 NDIS [ **NDIS\_状态\_PM\_卸载\_已拒绝**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-offload-rejected)状态指示通知设置已删除的协议的基础驱动程序将卸载。 **StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含已拒绝的协议卸载标识符协议卸载。 NDIS 提供中的协议卸载标识符**ProtocolOffloadId**的成员[ **NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构。

 

 





