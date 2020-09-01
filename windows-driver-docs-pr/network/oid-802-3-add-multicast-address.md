---
title: OID_802_3_ADD_MULTICAST_ADDRESS
description: 作为设置请求，NDIS 和过量协议驱动程序使用 OID_802_3_ADD_MULTICAST_ADDRESS OID 请求将802.3 多播地址添加到微型端口适配器的多播地址列表。
ms.assetid: e3e6defe-e65f-46bb-9cd6-cb65ffa7d7f0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_802_3_ADD_MULTICAST_ADDRESS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b2e2739648ebe9351d629860b3a743dd2554cf0f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217525"
---
# <a name="oid_802_3_add_multicast_address"></a>OID \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址


作为设置请求，NDIS 和过量协议驱动程序使用 OID \_ 802 \_ 3 \_ ADD \_ 多播 \_ address OID 请求将802.3 多播地址添加到微型端口适配器的多播地址列表。 多播地址是6个字节的数组。 添加地址后，该地址可接收多播数据包。

**版本信息**

<a href="" id="windows-vista"></a>Windows Vista  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a name="remarks"></a>备注
-------

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含6个字节的地址，该地址将添加到多播地址列表。

OID \_ 802 \_ 3 \_ ADD \_ 多播 \_ ADDRESS OID 请求只能添加一个地址。 若要添加多个地址，过量驱动程序必须发出多个 OID \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址 OID 请求。

NDIS 微型端口驱动程序不会直接接收此 OID 请求。 相反，NDIS 将每个 OID \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址和 [oid \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址](oid-802-3-delete-multicast-address.md) OID 请求合并为一个 [oid \_ 802 \_ 3 \_ 多播 \_ 列表](oid-802-3-multicast-list.md) OID 请求，并将其发送到微型端口驱动程序。

若要接收多播数据包，生成的驱动程序必须使用 [OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](oid-gen-current-packet-filter.md) OID 来设置数据包筛选器 **NDIS \_ 数据包 \_ 类型 \_ 多播** 标志。

小型端口驱动程序可以对多播地址列表可以包含的多路广播地址设置限制。 若要指定最大多播地址数，微型端口驱动程序将设置其传递给[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**MaxMulticastListSize**成员。 对于基于 NDIS 6.0 之前的 NDIS 版本的微型端口驱动程序，NDIS 通过发送 [oid \_ 802 \_ 3 \_ 最大 \_ 列表 \_ 大小](oid-802-3-maximum-list-size.md) oid 请求来查询多播地址的最大数目。 如果 OID **802 \_ \_ \_ ** \_ \_ 3 \_ 添加 \_ 多播 \_ 地址请求超出此限制，ndis 返回 ndis 状态多播已满。

若要删除以前添加的多播地址，请使用 [OID \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址](oid-802-3-delete-multicast-address.md) OID 来创建设置请求。 过量驱动程序可以多次添加给定的多播地址。 如果 NDIS 成功执行了给定多播地址的第一个 add 请求，NDIS 将成功对该地址的所有后续添加请求。 若要删除多次添加的多播地址，则过量驱动程序必须删除地址，使其添加地址的次数相同。

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


[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[OID \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址](oid-802-3-delete-multicast-address.md)

[OID \_ 802 \_ 3 \_ 最大 \_ 列表 \_ 大小](oid-802-3-maximum-list-size.md)

[OID \_ 802 \_ 3 \_ 多播 \_ 列表](oid-802-3-multicast-list.md)

[OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](oid-gen-current-packet-filter.md)

 

