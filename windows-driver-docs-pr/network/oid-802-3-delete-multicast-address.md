---
title: OID_802_3_DELETE_MULTICAST_ADDRESS
description: 作为设置请求，NDIS 和过量协议驱动程序使用 OID_802_3_DELETE_MULTICAST_ADDRESS OID 从微型端口适配器的多播地址列表中删除以前添加的多播地址。
ms.assetid: 5efaa724-80b4-4721-a1b0-8ba67c03bb32
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_802_3_DELETE_MULTICAST_ADDRESS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a320b3d4147ac878336a12dd5a6394073f8a0b0b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107326"
---
# <a name="oid_802_3_delete_multicast_address"></a>OID \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址


作为设置请求，NDIS 和过量协议驱动程序使用 OID \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址 OID 从微型端口适配器的多播地址列表中删除以前添加的多播地址。 多播地址是6个字节的数组。 删除某个地址将禁用该地址，使其无法再接收多播数据包。

**版本信息**

<a href="" id="windows-vista"></a>Windows Vista  
。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a name="remarks"></a>注解
-------

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含要从多播地址列表中删除的6个字节的地址。

OID \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址 OID 请求只能删除一个地址。 若要删除多个地址，协议驱动程序必须发出多个 OID \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址 OID 请求。

NDIS 微型端口驱动程序不会直接接收此 OID 请求。 相反，NDIS 合并每个 [oid \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址](oid-802-3-add-multicast-address.md) ，oid \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址 OID 请求到单个 [OID \_ 802 \_ 3 \_ 多播 \_ 列表](oid-802-3-multicast-list.md) OID 请求。

若要替换或删除整个多播列表，协议驱动程序可以使用 [oid \_ 802 \_ 3 \_ 多播 \_ 列表](oid-802-3-multicast-list.md) oid 请求。

若要将地址添加到列表中，协议驱动程序可以使用 [OID \_ 802 \_ 3 \_ add \_ 多播 \_ address](oid-802-3-add-multicast-address.md) OID 请求。

过量协议驱动程序可以通过发送多个 [OID \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址](oid-802-3-add-multicast-address.md) OID 请求，多次添加给定的多播地址。 如果 NDIS 成功执行了给定多播地址的第一个 add 请求，NDIS 将成功对该地址的所有后续添加请求。 若要删除多次添加的多播地址，则过量驱动程序必须删除地址，使其添加地址的次数相同。

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
<th>说明</th>
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
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址](oid-802-3-add-multicast-address.md)

[OID \_ 802 \_ 3 \_ 最大 \_ 列表 \_ 大小](oid-802-3-maximum-list-size.md)

[OID \_ 802 \_ 3 \_ 多播 \_ 列表](oid-802-3-multicast-list.md)

