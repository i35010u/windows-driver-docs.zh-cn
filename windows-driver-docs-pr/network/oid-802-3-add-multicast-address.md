---
title: OID_802_3_ADD_MULTICAST_ADDRESS
description: 作为设置请求，NDIS 和过量协议驱动程序使用 OID_802_3_ADD_MULTICAST_ADDRESS OID 请求将802.3 多播地址添加到微型端口适配器的多播地址列表。
ms.assetid: e3e6defe-e65f-46bb-9cd6-cb65ffa7d7f0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_802_3_ADD_MULTICAST_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 00843282c99f4673ff3426a42adf6fab2d00afd4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834568"
---
# <a name="oid_802_3_add_multicast_address"></a>OID\_802\_3\_添加\_多播\_地址


作为设置请求，NDIS 和过量协议驱动程序使用 OID\_802\_3\_添加\_多播\_ADDRESS OID 请求，以将802.3 多播地址添加到微型端口适配器的多播地址列表。 多播地址是6个字节的数组。 添加地址后，该地址可接收多播数据包。

**版本信息**

<a href="" id="windows-vista"></a>Windows Vista  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a name="remarks"></a>备注
-------

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含6个字节的地址，该地址将添加到多播地址列表。

OID\_802\_3\_添加\_多播\_地址 OID 请求只能添加一个地址。 要添加多个地址，过量驱动程序必须发出多个 OID\_802\_3\_添加\_多播\_地址 OID 请求。

NDIS 微型端口驱动程序不会直接接收此 OID 请求。 相反，NDIS 合并每个 OID 序列\_802\_3\_添加\_多播\_地址和[OID\_802\_3\_删除\_多播\_](oid-802-3-delete-multicast-address.md) [OID\_802\_3\_多播\_列表](oid-802-3-multicast-list.md)OID 请求，该请求将发送到微型端口驱动程序。

要接收多播数据包，生成的驱动程序必须使用[OID\_GEN\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)oid，将数据包筛选器**NDIS\_\_类型\_多播**标志。

小型端口驱动程序可以对多播地址列表可以包含的多路广播地址设置限制。 若要指定最大多播地址数，小型端口驱动程序会将 NDIS\_微型端口的**MaxMulticastListSize**成员设置[ **\_适配器\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)将其传递到[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数。 对于基于 NDIS 6.0 之前的 NDIS 版本的微型端口驱动程序，NDIS 通过发送[oid\_802\_3\_最大\_列表\_大小](oid-802-3-maximum-list-size.md)OID 请求来查询最大多播地址数。 如果 OID\_802\_3\_添加\_多播\_ADDRESS 请求超出此限制，NDIS 将 **\_多播\_FULL 返回 ndis\_状态**。

若要删除以前添加的多播地址，请使用[OID\_802\_3\_delete\_多播\_address](oid-802-3-delete-multicast-address.md) OID 来创建设置请求。 过量驱动程序可以多次添加给定的多播地址。 如果 NDIS 成功执行了给定多播地址的第一个 add 请求，NDIS 将成功对该地址的所有后续添加请求。 若要删除多次添加的多播地址，则过量驱动程序必须删除地址，使其添加地址的次数相同。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[OID\_802\_3\_删除\_多播\_地址](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_最大\_列表\_大小](oid-802-3-maximum-list-size.md)

[OID\_802\_3\_多播\_列表](oid-802-3-multicast-list.md)

[OID\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)

 

 




