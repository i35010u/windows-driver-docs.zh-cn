---
title: 筛选器模块直接 OID 请求
description: 筛选器模块直接 OID 请求
ms.assetid: 0ab7079b-6578-4932-a276-40a961b55efe
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec7f1ebe51126c18bab98fa63d22b2d378a30f0
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103770"
---
# <a name="filter-module-direct-oid-requests"></a>筛选器模块直接 OID 请求





为了支持直接 OID 请求路径，筛选器驱动程序在[**NDIS \_ 筛选器 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)结构中提供*FilterXxx*函数入口点，Ndis 为筛选器驱动程序提供**NdisF * Xxx*** 函数。

*直接 OID 请求接口*类似于标准 OID 请求接口。 例如， [**NdisFDirectOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequest) 和 [*FilterDirectOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request) 函数类似于 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 和 [*FilterOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request) 函数。

**注意**   NDIS 6.1 和更高版本支持用于直接 OID 请求接口的特定 Oid。 不支持在 NDIS 6.1 和某些 NDIS 6.1 Oid 之前存在的 Oid。 若要确定 OID 是否可用于直接 Oid 接口，请参阅 "OID 引用" 页。 例如，请参阅 [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md) OID 中的说明。

 

筛选器驱动程序必须能够处理未序列化的直接 OID 请求。 与标准 OID 请求接口不同，NDIS 不会将直接 OID 请求与通过直接 OID 接口或标准 OID 请求接口发送的其他请求进行序列化。 此外，筛选器驱动程序必须能够以 IRQL = 调度级别处理直接 OID 请求 &lt; \_ 。

若要支持直接 Oid 请求接口，请使用标准 OID 请求接口的文档。 下表显示了直接 OID 请求接口中的函数与标准 OID 请求接口之间的关系。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">直接 OID 函数</th>
<th align="left">标准 OID 函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request" data-raw-source="[&lt;em&gt;FilterDirectOidRequest&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request)"><em>FilterDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request" data-raw-source="[&lt;em&gt;FilterOidRequest&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)"><em>FilterOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_direct_oid_request" data-raw-source="[&lt;em&gt;FilterCancelDirectOidRequest&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_direct_oid_request)"><em>FilterCancelDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_oid_request" data-raw-source="[&lt;em&gt;FilterCancelOidRequest&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_oid_request)"><em>FilterCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request_complete" data-raw-source="[&lt;em&gt;FilterDirectOidRequestComplete&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_direct_oid_request_complete)"><em>FilterDirectOidRequestComplete</em></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete" data-raw-source="[&lt;em&gt;FilterOidRequestComplete&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)"><em>FilterOidRequestComplete</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequest" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequest)"><strong>NdisFDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest" data-raw-source="[&lt;strong&gt;NdisFOidRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)"><strong>NdisFOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequestcomplete)"><strong>NdisFDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisFDirectOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdirectoidrequestcomplete)"><strong>NdisFDirectOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcanceldirectoidrequest" data-raw-source="[&lt;strong&gt;NdisFCancelDirectOidRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcanceldirectoidrequest)"><strong>NdisFCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcanceloidrequest" data-raw-source="[&lt;strong&gt;NdisFCancelOidRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcanceloidrequest)"><strong>NdisFCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

