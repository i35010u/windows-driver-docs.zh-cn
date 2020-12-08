---
title: OID_802_3_MULTICAST_LIST
description: 作为集请求，NDIS 和过量协议驱动程序使用 OID_802_3_MULTICAST_LIST OID 请求来替换微型端口适配器上的当前多播地址列表。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_802_3_MULTICAST_LIST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 588d92bea79d9eae2e3aa875df67d269627b6697
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783801"
---
# <a name="oid_802_3_multicast_list"></a>OID \_ 802 \_ 3 \_ 多播 \_ 列表


作为设置请求，NDIS 和过量协议驱动程序使用 OID \_ 802 \_ 3 \_ 多播 \_ 列表 oid 请求来替换微型端口适配器上的当前多播地址列表。 如果地址在列表中存在，则将启用该地址以接收多播数据包。

作为查询请求，NDIS 和协议驱动程序使用 OID \_ 802 \_ 3 \_ 多播 \_ 列表 oid 请求来获取当前的多播地址列表。




NDIS 处理 \_ \_ \_ \_ 微型端口驱动程序的 OID 802 3 多播列表查询请求，因此小型端口驱动程序永远不会收到这些查询请求。

支持多播地址列表的微型端口驱动程序必须支持 OID \_ 802 \_ 3 \_ 多播 \_ 列表集请求。

对于集请求， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含多播地址列表作为地址数组。

-   每个地址都是一个6字节的数组。
-   **InformationBufferLength** 成员包含 **InformationBuffer** 数组的长度（以字节为单位）。
-   如果 **InformationBuffer** 成员的列表中存在重复地址，NDIS 会在 \_ \_ \_ \_ 向微型端口驱动程序发送 OID 802 3 多播列表集请求之前删除重复项。
-   如果 **InformationBufferLength** 成员为零，微型端口驱动程序必须清除多播地址列表。
-   如果 **InformationBufferLength** 成员大于零，则微型端口驱动程序必须将任何现有的多播地址列表替换为 **InformationBuffer** 成员的列表。

小型端口适配器的多播地址列表由绑定到微型端口适配器的所有协议驱动程序共享。 NDIS 控制对此列表的访问。 如果多个协议驱动程序尝试同时修改列表，NDIS 会将其请求合并为一个 OID \_ 802 \_ 3 \_ 多播 \_ 列表集请求，并将其发送到微型端口驱动程序。

初始化微型端口适配器后，它会重置 NIC，因此多播地址列表为零。 NDIS 还会初始化数据包筛选器，因此不允许协议驱动程序接收多播数据包。

若要接收多播数据包，协议驱动程序稍后必须执行以下操作之一：

-   将数据包筛选器设置为包括 **NDIS \_ 数据包 \_ 类型 \_ 多播** 标志。 无论何时，都可以通过取消此标志来禁用多播数据包接收。 协议驱动程序为多播数据包启用接收的顺序并不重要。 有关详细信息，请参阅 [OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](oid-gen-current-packet-filter.md) OID 请求。
-   将数据包筛选器设置为包括 **NDIS \_ 数据包 \_ 类型 " \_ 所有 \_ 多播** " 标志，这将启用所有多播数据包，并进行筛选本身。

小型端口驱动程序可以对多播地址列表可以包含的多路广播地址设置限制。 如果协议驱动程序超过此限制或指定了无效的多播地址，NDIS 将返回 **ndis \_ 状态 \_ 多播已 \_ 满** 。

对于查询请求，NDIS 返回多播地址列表，它是所有协议绑定的所有多播地址列表的联合。

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

[OID \_ 802 \_ 3 \_ 最大 \_ 列表 \_ 大小](oid-802-3-maximum-list-size.md)

[OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](oid-gen-current-packet-filter.md)

 

