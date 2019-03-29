---
title: OID_802_3_ADD_MULTICAST_ADDRESS
description: 为 set 请求，NDIS 和基础协议驱动程序使用 OID_802_3_ADD_MULTICAST_ADDRESS OID 请求向 802.3 的多播的地址的微型端口适配器多路广播的地址列表。
ms.assetid: e3e6defe-e65f-46bb-9cd6-cb65ffa7d7f0
ms.date: 08/08/2017
keywords: -OID_802_3_ADD_MULTICAST_ADDRESS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c9ba8b1e689d3ce2ce190a0967ae58f29dd428ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567823"
---
# <a name="oid8023addmulticastaddress"></a>OID\_802\_3\_添加\_多播\_地址


为 set 请求，NDIS 和基础协议驱动程序使用 OID\_802\_3\_添加\_多播\_将 802.3 的多播的地址添加到多播的地址列表的微型端口地址 OID 请求适配器。 多播的地址是 6 个字节的数组。 添加一个地址，该地址以接收多路广播的数据包。

**版本信息**

<a href="" id="windows-vista"></a>Windows Vista  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a name="remarks"></a>备注
-------

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含要添加到多路广播的 6 个字节地址地址列表。

OID\_802\_3\_添加\_多播\_地址 OID 请求可以添加只能有一个地址。 若要添加多个地址，基础驱动程序必须发出多个 OID\_802\_3\_添加\_多播\_地址 OID 请求。

NDIS 微型端口驱动程序不直接接收此 OID 请求。 相反，NDIS 将合并每个序列的 OID\_802\_3\_添加\_多播\_地址并[OID\_802\_3\_删除\_多播\_地址](oid-802-3-delete-multicast-address.md)OID 请求到单个[OID\_802\_3\_多播\_列表](oid-802-3-multicast-list.md)OID 请求，将其发送到微型端口驱动程序。

若要接收多路广播的数据包，基础驱动程序必须使用[OID\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)OID 设置数据包筛选器**NDIS\_数据包\_类型\_多播**标志。

微型端口驱动程序可以在数量的多播的地址列表可以包含的多播地址上设置限制。 若要指定的最大的多播地址，微型端口驱动程序集**MaxMulticastListSize**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构，它将传递给[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。 对于基于 NDIS 6.0 之前的 NDIS 版本的微型端口驱动程序，NDIS 所查询的通过发送的多播地址的最大数目[OID\_802\_3\_最大\_列表\_大小](oid-802-3-maximum-list-size.md) OID 请求。 返回 NDIS **NDIS\_状态\_多播\_完整**如果 OID\_802\_3\_添加\_多播\_地址请求超出此限制。

若要删除以前添加的多路广播的地址，请使用 set 请求[OID\_802\_3\_删除\_多播\_地址](oid-802-3-delete-multicast-address.md)OID。 基础驱动程序可以多次添加给定的多播的地址。 如果 NDIS 成功为给定的多播地址的第一个添加请求，NDIS 将成功执行所有后续添加该地址的请求。 若要删除已超过一次添加一个多播的地址，基础驱动程序必须删除的地址的地址，添加相同次数。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[OID\_802\_3\_DELETE\_MULTICAST\_ADDRESS](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_MAXIMUM\_LIST\_SIZE](oid-802-3-maximum-list-size.md)

[OID\_802\_3\_MULTICAST\_LIST](oid-802-3-multicast-list.md)

[OID\_GEN\_CURRENT\_PACKET\_FILTER](oid-gen-current-packet-filter.md)

 

 




