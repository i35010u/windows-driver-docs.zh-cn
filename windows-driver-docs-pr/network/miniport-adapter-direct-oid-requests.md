---
title: 微型端口适配器直接 OID 请求
description: 微型端口适配器直接 OID 请求
ms.assetid: 63ced5a3-0c83-4952-aa0e-c3c654b3f241
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eb95533a1607bbd3ad53b461eb41530b65c7d0b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373963"
---
# <a name="miniport-adapter-direct-oid-requests"></a>微型端口适配器直接 OID 请求





若要支持直接的 OID 请求路径，微型端口驱动程序提供*MiniportXxx*中的函数入口点[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构和 NDIS 提供**NdisM * Xxx*** 微型端口驱动程序的函数。

*直接 OID 请求接口*类似于标准的 OID 请求接口。 例如， [ **NdisMDirectOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismdirectoidrequestcomplete)并[ *MiniportDirectOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_direct_oid_request)函数是类似于[**NdisMOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)并[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数。

**请注意**  NDIS 6.1 支持特定 Oid 与 direct 的 OID 请求接口一起使用。 不支持 NDIS 6.1 和一些 NDIS 6.1 Oid 之前即已存在的 Oid。 若要确定是否可以直接 Oid 界面中使用 OID，请参阅 OID 引用页。 

微型端口驱动程序必须能够处理不会序列化的直接 OID 请求。 与标准的 OID 请求接口，不同 NDIS 不序列化与使用直接的 OID 接口或使用标准的 OID 请求接口发送其他请求直接 OID 请求。 此外，微型端口驱动程序必须能够处理直接 OID 请求在 IRQL &lt;= 调度\_级别。

若要支持直接的 Oid 请求接口，使用标准的 OID 请求接口的文档。 下表显示了直接的 OID 请求接口中的函数和标准的 OID 请求接口之间的关系。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_direct_oid_request" data-raw-source="[&lt;em&gt;MiniportDirectOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_direct_oid_request)"><em>MiniportDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request" data-raw-source="[&lt;em&gt;MiniportOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)"><em>MiniportOidRequest</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_direct_oid_request" data-raw-source="[&lt;em&gt;MiniportCancelDirectOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_direct_oid_request)"><em>MiniportCancelDirectOidRequest</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_oid_request" data-raw-source="[&lt;em&gt;MiniportCancelOidRequest&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_oid_request)"><em>MiniportCancelOidRequest</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismdirectoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMDirectOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismdirectoidrequestcomplete)"><strong>NdisMDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





