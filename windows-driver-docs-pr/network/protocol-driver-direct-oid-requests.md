---
title: 协议驱动程序直接 OID 请求
description: 协议驱动程序直接 OID 请求
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e61a1e51eff62804590b651dfe46f4bb64c9e90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797917"
---
# <a name="protocol-driver-direct-oid-requests"></a>协议驱动程序直接 OID 请求





为了支持直接 OID 请求路径，协议驱动程序在 [**ndis \_ 协议 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_driver_characteristics)结构中提供 *ProtocolXxx* 函数入口点，ndis 为协议驱动程序提供 **ndis * Xxx*** 函数。

*直接 OID 请求接口* 类似于标准 OID 请求接口。 例如， [**NdisDirectOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdirectoidrequest) 和 [**ProtocolDirectOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_direct_oid_request_complete) 函数类似于 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 和 [**ProtocolOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete) 函数。

**注意**  NDIS 6.1 和更高版本支持用于直接 OID 请求接口的特定 Oid。 不支持在 NDIS 6.1 和某些 NDIS 6.1 Oid 之前存在的 Oid。 若要确定 OID 是否可用于直接 Oid 接口，请参阅 "OID 引用" 页。 例如，请参阅 [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md) OID 中的说明。

 

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_direct_oid_request_complete" data-raw-source="[&lt;strong&gt;ProtocolDirectOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_direct_oid_request_complete)"><strong>ProtocolDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete" data-raw-source="[&lt;strong&gt;ProtocolOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_oid_request_complete)"><strong>ProtocolOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdirectoidrequest" data-raw-source="[&lt;strong&gt;NdisDirectOidRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdirectoidrequest)"><strong>NdisDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest" data-raw-source="[&lt;strong&gt;NdisOidRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)"><strong>NdisOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceldirectoidrequest" data-raw-source="[&lt;strong&gt;NdisCancelDirectOidRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceldirectoidrequest)"><strong>NdisCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest" data-raw-source="[&lt;strong&gt;NdisCancelOidRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest)"><strong>NdisCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

