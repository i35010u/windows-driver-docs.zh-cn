---
title: 处理 CoNDIS WAN 微型端口驱动程序中的查询
description: 处理 CoNDIS WAN 微型端口驱动程序中的查询
ms.assetid: 634618ce-3168-4729-b74a-e69f27b62ef4
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，查询处理
- OID_WAN_CO_GET_INFO
- OID_WAN_CO_GET_LINK_INFO
- OID_WAN_CO_GET_STATS_INFO
- 查询 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e8626491c3819290ee9ccc153616c55de3f74c3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107494"
---
# <a name="handling-queries-in-a-condis-wan-miniport-driver"></a>处理 CoNDIS WAN 微型端口驱动程序中的查询





本主题概述了在 CoNDIS WAN 微型端口驱动程序中处理查询的要求。 上层驱动程序使用查询请求来调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) ，以确定 CoNDIS wan 微型端口驱动程序和微型端口驱动程序 NIC 的特定于 wan 的功能和当前状态。

NDISWAN 中间驱动程序转发查询请求后，NDIS 将调用微型端口驱动程序的 [**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数。 在 CoNDIS WAN 微型端口驱动程序中，此函数与任何面向连接的微型端口驱动程序相同，只是 CoNDIS WAN 微型端口驱动程序支持 [CONDIS WAN 对象](/windows-hardware/drivers/ddi/ntddndis/index)。

如果 CoNDIS WAN 微型端口驱动程序通过返回 NDIS 状态 "挂起" 的状态以异步方式完成 *MiniportCoOidRequest* \_ \_ ，则它必须在稍后通过调用 [**NdisCoOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)来完成查询。

当 NDIS 调用 *MiniportCoOidRequest*时，ndis 会传递一个指向 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构的指针，该结构包含查询 OID 和一个缓冲区，用于保存从微型端口驱动程序中检索到的信息。 微型端口驱动程序控制此缓冲区，直到请求完成。 如果在 NDIS oid 请求的 **InformationBufferLength** 成员中指定的字节 \_ 数 \_ 不足以满足 oid 所需的信息，则微型端口驱动程序应使查询请求失败，并将 NDIS OID 请求的 **BytesNeeded** 成员设置 \_ \_ 为 OID 所需的字节数。

在当前查询请求完成之前，不会将其他请求提交到特定 WAN 微型端口驱动程序。

下表总结了用于获取或设置 CoNDIS WAN 微型端口驱动程序的操作特征的 Oid。

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
<a href="/windows-hardware/drivers/network/oid-wan-co-get-info" data-raw-source="[OID_WAN_CO_GET_INFO](./oid-wan-co-get-info.md)">OID_WAN_CO_GET_INFO</a> 获取有关 (VCs) 的虚拟连接的信息。</td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<a href="/windows-hardware/drivers/network/oid-wan-co-get-link-info" data-raw-source="[OID_WAN_CO_GET_LINK_INFO](./oid-wan-co-get-link-info.md)">OID_WAN_CO_GET_LINK_INFO</a> 获取有关 VC 的信息。</td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<a href="/windows-hardware/drivers/network/oid-wan-co-get-stats-info" data-raw-source="[OID_WAN_CO_GET_STATS_INFO](./oid-wan-co-get-stats-info.md)">OID_WAN_CO_GET_STATS_INFO</a> 获取 VC 的统计信息。</td>
<td align="left"><p>可选</p></td>
</tr>
</tbody>
</table>

 

CoNDIS WAN 微型端口驱动程序可以支持所有 NDIS [常规对象](/previous-versions/windows/hardware/network/ff546510(v=vs.85))。 若要了解有关在 CoNDIS 微型端口驱动程序中设置信息的详细信息，请参阅 [查询或设置信息](querying-or-setting-information.md)。

