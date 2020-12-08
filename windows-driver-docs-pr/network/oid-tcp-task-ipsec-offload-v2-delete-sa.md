---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA
description: 作为集，TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA OID 来请求微型端口驱动程序从 NIC (SAs) 删除指定的安全关联。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a5f99f437f6f157bb33deaa5fbdee32980d15fe9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808589"
---
# <a name="oid_tcp_task_ipsec_offload_v2_delete_sa"></a>OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ DELETE \_ SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组设置，TCP/IP 传输使用 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ delete \_ SA OID 来请求微型端口驱动程序从 NIC)  (SAs 中删除指定的安全关联。

**注意**  NDIS 支持直接 OID 请求接口的此 OID。 有关直接 OID 请求接口的详细信息，请参阅 [NDIS 6.1 直接 Oid 请求接口](/windows-hardware/drivers/ddi/_netvista/)。

 

<a name="remarks"></a>备注
-------

所有支持 IPsec 卸载版本 2 (IPsecOV2) 的 NDIS 6.1 微型端口驱动程序必须支持此 OID。

当微型端口驱动程序收到此请求时，驱动程序应从 NIC 中删除指定的 SAs，并释放为 SAs 分配的任何系统资源。

微型端口驱动程序接收 [**IPSEC \_ 卸载 \_ V2 \_ 删除 \_ SA**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_delete_sa) 结构，其中包含 SA 绑定的句柄，并接收指向链接列表中下一个 **IPSEC \_ 卸载 \_ V2 \_ 删除 \_ sa** 结构的指针。

微型端口驱动程序可以在 "接收 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构" 的 " [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)结构" 中设置 **SaDeleteReq** 。 接下来，TCP/IP 传输会发出 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ delete \_ sa，以便删除接收数据包的入站 sa，并再次删除与已删除的入站 sa 相对应的出站 sa。 在接收相应的 OID \_ TCP \_ 任务 " \_ IPSEC \_ 卸载 \_ V2" \_ \_ 请求之前，NIC 不得删除其中的任何一种 SAs。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数为此请求返回以下值之一：

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
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a> 函数来成功请求，同时传递 <strong>NDIS_STATUS_SUCCESS</strong> 的 <em>状态</em> 参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>正在重置微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，NDIS 称为 <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>MiniportResetEx</em></a> 函数。</p></td>
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IPSEC \_ 卸载 \_ V2 \_ 删除 \_ SA**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_delete_sa)

[**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)

[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

