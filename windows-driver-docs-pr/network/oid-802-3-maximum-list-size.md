---
title: OID_802_3_MAXIMUM_LIST_SIZE
description: OID_802_3_MAXIMUM_LIST_SIZE
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_802_3_MAXIMUM_LIST_SIZE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 29721b97411394e6850741663f3e950a277584a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783811"
---
# <a name="oid_802_3_maximum_list_size"></a>OID \_ 802 \_ 3 \_ 最大 \_ 列表 \_ 大小





NDIS 和过量协议驱动程序使用 OID \_ 802 \_ 3 \_ 最大 \_ 列表 \_ 大小 oid 请求来查询或设置微型端口适配器的多路广播地址列表可容纳的6字节多播地址的最大数目。

此多播地址列表由绑定到微型端口适配器的所有协议驱动程序共享。 由于它是共享资源，因此协议驱动程序可以从微型端口适配器接收 **NDIS \_ 状态 \_ 多播 \_** ，以响应 [oid \_ 802 \_ 3 \_ 多播 \_ 列表](oid-802-3-multicast-list.md) OID 集请求，即使列表中的元素数目小于前面为 oid \_ 802 \_ 3 \_ 最大 \_ 列表 \_ 大小 oid 查询请求返回的值，也是如此。

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

## <a name="see-also"></a>请参阅


[OID \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址](oid-802-3-add-multicast-address.md)

[OID \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址](oid-802-3-delete-multicast-address.md)

[OID \_ 802 \_ 3 \_ 多播 \_ 列表](oid-802-3-multicast-list.md)

 

 




