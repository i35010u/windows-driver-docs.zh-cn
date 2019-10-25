---
title: 设置 CoNDIS WAN 微型端口驱动程序信息
description: 设置 CoNDIS WAN 微型端口驱动程序信息
ms.assetid: 950cb2cb-7f02-4f3c-924a-0d1e7bb19b55
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，信息设置
- OID_WAN_CO_SET_LINK_INFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1cb23df349f54cb98c735e9c6b4cc6296a07ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841947"
---
# <a name="setting-condis-wan-miniport-driver-information"></a>设置 CoNDIS WAN 微型端口驱动程序信息





本主题概述了在 CoNDIS WAN 微型端口驱动程序中设置信息的要求。 上层驱动程序使用 set 请求来调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) ，以更改 CoNDIS WAN 微型端口驱动程序和微型端口驱动程序 NIC 维护的信息。

NDISWAN 中间驱动程序转发 set 请求后，NDIS 将调用 WAN 微型端口驱动程序的[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数。 在 CoNDIS WAN 微型端口驱动程序中，此函数与任何 CoNDIS 微型端口驱动程序中的相同，只不过 CoNDIS WAN 微型端口驱动程序支持[CONDIS WAN 对象](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)。

在完成当前的 set 请求之前，不会将其他请求提交到 CoNDIS WAN 微型端口驱动程序。 如果微型端口驱动程序不会立即完成设置请求，它将从*MiniportCoOidRequest*返回 NDIS\_状态\_挂起，然后必须调用[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)来完成请求。

CoNDIS WAN 微型端口驱动程序必须识别并正确响应以下 CoNDIS WAN Oid。

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
<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-set-link-info" data-raw-source="[OID_WAN_CO_SET_LINK_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-set-link-info)">OID_WAN_CO_SET_LINK_INFO</a>设置 VC 的信息。</td>
<td align="left"><p>必需</p></td>
</tr>
</tbody>
</table>

 

CoNDIS WAN 微型端口驱动程序还支持 NDIS[常规对象](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))。 若要了解有关在 CoNDIS 微型端口驱动程序中设置信息的详细信息，请参阅[查询或设置信息](querying-or-setting-information.md)。

 

 





