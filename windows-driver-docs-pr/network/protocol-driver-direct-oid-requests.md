---
title: 协议驱动程序直接 OID 请求
description: 协议驱动程序直接 OID 请求
ms.assetid: 387d27de-3214-4f93-8f45-9a2f28e5036f
keywords:
- 直接 OID 请求接口 WDK 网络
- 直接 OID 请求路径 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d5655549105827ff61f7392e1aa832869b8e0ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385458"
---
# <a name="protocol-driver-direct-oid-requests"></a>协议驱动程序直接 OID 请求





若要支持直接的 OID 请求路径，协议驱动程序提供*ProtocolXxx*中的函数入口点[ **NDIS\_协议\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_driver_characteristics)结构和 NDIS 提供**Ndis * Xxx*** 协议驱动程序的函数。

*直接 OID 请求接口*类似于标准的 OID 请求接口。 例如， [ **NdisDirectOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisdirectoidrequest)并[ **ProtocolDirectOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_direct_oid_request_complete)函数是类似于[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)并[ **ProtocolOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_oid_request_complete)函数。

**请注意**  NDIS 6.1 和更高版本支持特定 Oid 用于直接 OID 请求接口。 不支持 NDIS 6.1 和一些 NDIS 6.1 Oid 之前即已存在的 Oid。 若要确定是否可以直接 Oid 界面中使用 OID，请参阅 OID 引用页。 有关示例，请参阅中的说明[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) OID。

 

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_direct_oid_request_complete" data-raw-source="[&lt;strong&gt;ProtocolDirectOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_direct_oid_request_complete)"><strong>ProtocolDirectOidRequestComplete</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_oid_request_complete" data-raw-source="[&lt;strong&gt;ProtocolOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_oid_request_complete)"><strong>ProtocolOidRequestComplete</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisdirectoidrequest" data-raw-source="[&lt;strong&gt;NdisDirectOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisdirectoidrequest)"><strong>NdisDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest" data-raw-source="[&lt;strong&gt;NdisOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)"><strong>NdisOidRequest</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceldirectoidrequest" data-raw-source="[&lt;strong&gt;NdisCancelDirectOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceldirectoidrequest)"><strong>NdisCancelDirectOidRequest</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceloidrequest" data-raw-source="[&lt;strong&gt;NdisCancelOidRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceloidrequest)"><strong>NdisCancelOidRequest</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





