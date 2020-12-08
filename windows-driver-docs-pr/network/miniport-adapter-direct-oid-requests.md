---
title: 微型端口适配器直接 OID 请求
description: 微型端口适配器直接 OID 请求
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 249fbb6424ae729ff9340fe0112191773e491c5e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798069"
---
# <a name="miniport-adapter-direct-oid-requests"></a>微型端口适配器直接 OID 请求





为了支持直接 OID 请求路径，小型端口驱动程序在 [**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构中提供 *MiniportXxx* 函数入口点，Ndis 为微型端口驱动程序提供 **NdisM * Xxx*** 函数。

*直接 OID 请求接口* 类似于标准 OID 请求接口。 例如， [**NdisMDirectOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismdirectoidrequestcomplete) 和 [*MiniportDirectOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_direct_oid_request) 函数类似于 [**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete) 和 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数。

**注意**  NDIS 6.1 支持使用特定 Oid 与直接 OID 请求接口一起使用。 不支持在 NDIS 6.1 和某些 NDIS 6.1 Oid 之前存在的 Oid。 若要确定 OID 是否可用于直接 Oid 接口，请参阅 "OID 引用" 页。 

微型端口驱动程序必须能够处理未序列化的直接 OID 请求。 与标准 OID 请求接口不同，NDIS 不会将直接 OID 请求与通过直接 OID 接口或标准 OID 请求接口发送的其他请求进行序列化。 此外，微型端口驱动程序必须能够以 IRQL = 调度级别处理直接 OID 请求 &lt; \_ 。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_direct_oid_request" data-raw-source="[&lt;em&gt;MiniportDirectOidRequest&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_direct_oid_request)"><em>MiniportDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request" data-raw-source="[&lt;em&gt;MiniportOidRequest&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)"><em>MiniportOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_direct_oid_request" data-raw-source="[&lt;em&gt;MiniportCancelDirectOidRequest&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_direct_oid_request)"><em>MiniportCancelDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request" data-raw-source="[&lt;em&gt;MiniportCancelOidRequest&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request)"><em>MiniportCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismdirectoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMDirectOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismdirectoidrequestcomplete)"><strong>NdisMDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a></p></td>
</tr>
</tbody>
</table>

 

