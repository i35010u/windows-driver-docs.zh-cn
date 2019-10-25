---
title: OID_802_3_MULTICAST_LIST
description: 作为一个集请求，NDIS 和过量协议驱动程序使用 OID_802_3_MULTICAST_LIST OID 请求来替换微型端口适配器上的当前多播地址列表。
ms.assetid: 601f38e1-26ae-4d72-9d72-91bd58f81bba
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_802_3_MULTICAST_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 39e6ff3725355fdc798e6b2d01a127dd0416470a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834551"
---
# <a name="oid_802_3_multicast_list"></a>OID\_802\_3\_多播\_列表


作为设置请求，NDIS 和过量协议驱动程序使用 OID\_802\_3\_多播\_列表 OID 请求来替换微型端口适配器上的当前多播地址列表。 如果地址在列表中存在，则将启用该地址以接收多播数据包。

作为查询请求，NDIS 和协议驱动程序使用 OID\_802\_3\_多播\_列表 OID 请求以获取当前的多播地址列表。




NDIS 处理 OID\_802\_3\_多播\_列出微型端口驱动程序的查询请求，因此小型端口驱动程序永远不会收到这些查询请求。

支持多播地址列表的微型端口驱动程序必须支持 OID\_802\_3\_多播\_列表集请求。

对于集请求， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含多播地址列表作为地址数组。

-   每个地址都是一个6字节的数组。
-   **InformationBufferLength**成员包含**InformationBuffer**数组的长度（以字节为单位）。
-   如果**InformationBuffer**成员的列表中存在重复的地址，NDIS 会在向微型端口驱动程序发送 OID\_802\_3\_多播\_列表集请求之前删除重复项。
-   如果**InformationBufferLength**成员为零，微型端口驱动程序必须清除多播地址列表。
-   如果**InformationBufferLength**成员大于零，则微型端口驱动程序必须将任何现有的多播地址列表替换为**InformationBuffer**成员的列表。

小型端口适配器的多播地址列表由绑定到微型端口适配器的所有协议驱动程序共享。 NDIS 控制对此列表的访问。 如果多个协议驱动程序尝试同时修改列表，NDIS 会将其请求合并为一个 OID\_802\_3\_多播\_列表集请求，并将其发送到微型端口驱动程序。

初始化微型端口适配器后，它会重置 NIC，因此多播地址列表为零。 NDIS 还会初始化数据包筛选器，因此不允许协议驱动程序接收多播数据包。

若要接收多播数据包，协议驱动程序稍后必须执行以下操作之一：

-   将数据包筛选器设置为包括**NDIS\_数据包\_类型\_多播**标志。 无论何时，都可以通过取消此标志来禁用多播数据包接收。 协议驱动程序为多播数据包启用接收的顺序并不重要。 有关详细信息，请参阅[OID\_GEN\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)OID 请求。
-   将数据包筛选器设置为包括**NDIS\_数据包\_类型\_所有\_多播**标志，这将启用所有多播数据包，并执行筛选。

小型端口驱动程序可以对多播地址列表可以包含的多路广播地址设置限制。 如果协议驱动程序超过此限制或指定了无效的多播地址，NDIS 将 **\_多播\_FULL 返回 ndis\_状态**。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_802\_3\_添加\_多播\_地址](oid-802-3-add-multicast-address.md)

[OID\_802\_3\_删除\_多播\_地址](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_最大\_列表\_大小](oid-802-3-maximum-list-size.md)

[OID\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)

 

 




