---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA
description: 作为一组 TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA OID 请求微型端口驱动程序从 NIC 中删除指定的安全关联 (Sa)
ms.assetid: 9b2c702c-beaa-4caf-97c5-d80a2632e4d3
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c8dac562bbb94f93e5c1e6be09cfa1f79af6ac6c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353700"
---
# <a name="oidtcptaskipsecoffloadv2deletesa"></a>OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组 TCP/IP 传输使用 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA OID 以请求微型端口驱动程序删除指定的安全性关联 (Sa) 从一个 nic。

**请注意**  NDIS 支持此 OID 与 direct 的 OID 请求接口。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 OID 请求接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

 

<a name="remarks"></a>备注
-------

所有 NDIS 6.1 微型端口驱动程序支持 IPsec 都卸载版本 2 (IPsecOV2) 必须支持此 OID。

当微型端口驱动程序收到此请求时，该驱动程序应从 NIC 中删除指定的 SAs，并释放针对该 SAs 分配任何系统资源。

微型端口驱动程序收到[ **IPSEC\_卸载\_V2\_删除\_SA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ipsec_offload_v2_delete_sa)包含 SA 捆绑包的句柄和指向的结构下一步**IPSEC\_卸载\_V2\_删除\_SA**链接列表中的结构。

微型端口驱动程序可以设置**SaDeleteReq**中[ **NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)结构的接收[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 TCP/IP 传输随后发出 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA 一次来删除通过接收数据包的入站的 SA再一次删除对应于已删除的入站 SA 的出站 SA。 NIC 必须前未删除这些 SAs 任一接收相应的 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA 请求。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数将返回以下值之一用于此请求：

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
<td><p>微型端口驱动程序将以异步方式完成的请求。 微型端口驱动程序已完成所有处理后，它必须请求成功通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)"> <strong>NdisMOidRequestComplete</strong> </a>函数，传递<strong>NDIS_STATUS_SUCCESS</strong>对于<em>状态</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>微型端口驱动程序正在重置。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，名为 NDIS <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)"> <em>MiniportResetEx</em> </a>函数。</p></td>
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
<td><p>Version</p></td>
<td><p>支持 NDIS 6.1 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IPSEC\_OFFLOAD\_V2\_DELETE\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ipsec_offload_v2_delete_sa)

[**NDIS\_IPSEC\_OFFLOAD\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

 

 




