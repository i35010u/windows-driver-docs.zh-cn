---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA
description: 作为集，TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA OID 来请求微型端口驱动程序从 NIC 中删除指定的安全关联（SAs）。
ms.assetid: 9b2c702c-beaa-4caf-97c5-d80a2632e4d3
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aa796160d0667580eb9d4f4401fd5d7b6d524d8a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843886"
---
# <a name="oid_tcp_task_ipsec_offload_v2_delete_sa"></a>OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组设置，TCP/IP 传输使用 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_DELETE\_SA OID 来请求微型端口驱动程序从 NIC 中删除指定的安全关联（SAs）。

**请注意**  通过直接 OID 请求接口，NDIS 支持此 oid。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 Oid 请求接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

<a name="remarks"></a>备注
-------

所有支持 IPsec 卸载版本2（IPsecOV2）的 NDIS 6.1 微型端口驱动程序必须支持此 OID。

当微型端口驱动程序收到此请求时，驱动程序应从 NIC 中删除指定的 SAs，并释放为 SAs 分配的任何系统资源。

微型端口驱动程序接收[**IPSEC\_卸载\_V2\_删除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_delete_sa)包含 sa 捆绑的句柄的\_sa 结构，以及指向下一个**IPSEC\_卸载\_V2 的指针\_删除\_SA**链接列表中的结构。

微型端口驱动程序可以在[**NDIS\_IPSEC\_卸载\_V2 中设置 SaDeleteReq\_net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info) [ **\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)\_\_\_ 接下来，TCP/IP 传输\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA 一次，删除接收数据包的入站 SA，并再次删除出站 SA与已删除的入站 SA 相对应的。 在接收相应 OID 之前，NIC 不能删除其中的任何一种 SAs\_TCP\_任务\_IPSEC\_卸载\_V2\_DELETE\_SA 请求。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数为此请求返回以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>微型端口驱动程序已成功完成请求。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>函数来成功请求，同时传递<strong>NDIS_STATUS_SUCCESS</strong>的<em>状态</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>正在重置微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，NDIS 称为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>MiniportResetEx</em></a>函数。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.1 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IPSEC\_卸载\_V2\_删除\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_delete_sa)

[**NDIS\_IPSEC\_卸载\_V2\_NET\_缓存\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)

[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

 

 




