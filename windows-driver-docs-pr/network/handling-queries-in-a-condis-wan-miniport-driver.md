---
title: 处理 CoNDIS WAN 微型端口驱动程序中的查询
description: 处理 CoNDIS WAN 微型端口驱动程序中的查询
ms.assetid: 634618ce-3168-4729-b74a-e69f27b62ef4
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络、 查询处理
- OID_WAN_CO_GET_INFO
- OID_WAN_CO_GET_LINK_INFO
- OID_WAN_CO_GET_STATS_INFO
- WDK 的 CoNDIS WAN 的查询
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 940af1a1fadd00782d3c3bc86834cb4f8c452122
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366643"
---
# <a name="handling-queries-in-a-condis-wan-miniport-driver"></a>处理 CoNDIS WAN 微型端口驱动程序中的查询





本主题概述了用于处理查询中的 CoNDIS WAN 的微型端口驱动程序的要求。 上层驱动程序调用[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)与查询请求，以确定特定于 WAN 的功能和当前状态的 CoNDIS WAN 的微型端口驱动程序和微型端口驱动程序的 nic。

NDIS NDISWAN 中间驱动程序将转发查询请求后，调用微型端口驱动程序[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)函数。 此函数在 CoNDIS WAN 的微型端口驱动程序，是与任何面向连接的微型端口驱动程序中的相同，只不过 CoNDIS WAN 微型端口驱动程序支持[CoNDIS WAN 对象](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)。

如果 WAN 的 CoNDIS 微型端口驱动程序完成*MiniportCoOidRequest*以异步方式通过返回的状态为 NDIS\_状态\_挂起状态，则必须完成查询更高版本通过调用[ **NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)。

当调用 NDIS *MiniportCoOidRequest*，NDIS 将传递一个指向[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，其中包含查询 OID和用于保存从微型端口驱动程序检索的信息的缓冲区。 微型端口驱动程序控制此缓冲区，直到在请求完成。 如果在中指定的字节数**InformationBufferLength**成员的 NDIS\_OID\_请求是不够的 OID 要求的信息、 微型端口驱动程序应会使查询请求失败并设置**BytesNeeded**成员的 NDIS\_OID\_对 OID 需要的字节数的请求。

当前的查询请求完成之前，没有其他请求将提交到特定的 WAN 微型端口驱动程序。

下表总结了用于获取或设置的 CoNDIS WAN 微型端口驱动程序的操作特征的 Oid。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名称</th>
<th align="left">可选或必需</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-info" data-raw-source="[OID_WAN_CO_GET_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-info)">OID_WAN_CO_GET_INFO</a>获取有关虚拟连接 (VCs) 的信息。</td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-link-info" data-raw-source="[OID_WAN_CO_GET_LINK_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-link-info)">OID_WAN_CO_GET_LINK_INFO</a>获取 VC 有关的信息。</td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info" data-raw-source="[OID_WAN_CO_GET_STATS_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-stats-info)">OID_WAN_CO_GET_STATS_INFO</a>获取 VC 的统计信息。</td>
<td align="left"><p>可选</p></td>
</tr>
</tbody>
</table>

 

CoNDIS WAN 的微型端口驱动程序可以支持所有 NDIS[常规对象](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))。 若要了解有关的 CoNDIS 微型端口驱动程序中设置信息的详细信息，请参阅[查询或设置信息](querying-or-setting-information.md)。

 

 





