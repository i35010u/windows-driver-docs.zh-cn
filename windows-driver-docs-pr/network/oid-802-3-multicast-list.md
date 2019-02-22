---
title: OID_802_3_MULTICAST_LIST
description: 为 set 请求，NDIS 和基础协议驱动程序使用 OID_802_3_MULTICAST_LIST OID 请求替换微型端口适配器上的当前多路广播的地址列表。
ms.assetid: 601f38e1-26ae-4d72-9d72-91bd58f81bba
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_802_3_MULTICAST_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6e13042af3e6889852b9000fdd8ffe32e24358bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533361"
---
# <a name="oid8023multicastlist"></a>OID\_802\_3\_多播\_列表


为 set 请求，NDIS 和基础协议驱动程序使用 OID\_802\_3\_多播\_列表 OID 请求以更换微型端口适配器上的当前多路广播的地址列表。 如果在列表中存在一个地址，则已启用该地址来接收多路广播的数据包。

作为查询请求，NDIS 和协议驱动程序使用 OID\_802\_3\_多播\_列表 OID 请求以获取当前多路广播的地址列表。




NDIS 处理 OID\_802\_3\_多播\_列表查询的微型端口驱动程序，以便微型端口驱动程序永远不会接收这些请求查询请求。

支持多播的地址列表的微型端口驱动程序必须支持 OID\_802\_3\_多播\_列表设置的请求。

对于组的请求， **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含多播的地址列表地址的数组。

-   每个地址是 6 个字节的数组。
-   **InformationBufferLength**成员的包含的长度，以字节为单位， **InformationBuffer**数组。
-   如果在列表中有重复的地址**InformationBuffer**成员，NDIS 发送 OID 之前移除重复项\_802\_3\_多播\_列表设置为请求微型端口驱动程序。
-   如果**InformationBufferLength**成员为零，则微型端口驱动程序必须清除多路广播的地址列表。
-   如果**InformationBufferLength**成员是大于零，微型端口驱动程序必须将任何现有的多播的地址列表中的列表替换为**InformationBuffer**成员。

由绑定到的微型端口适配器的所有协议驱动程序共享的微型端口适配器多路广播的地址列表。 NDIS 控件访问此列表。 如果多个协议驱动程序尝试同时修改列表，NDIS 会将其请求合并到单个 OID\_802\_3\_多播\_列表设置请求中，将其发送到微型端口驱动程序。

初始化的微型端口适配器时，它重置 NIC 因此多播的地址列表是零。 NDIS 还将初始化数据包筛选器，以便它不允许协议驱动程序，以接收多路广播的数据包。

若要接收多路广播的数据包，协议驱动程序必须更高版本执行以下操作：

-   设置数据包筛选器，包括**NDIS\_数据包\_类型\_多播**标志。 在任何时候，它可以通过取消此标志来禁止多路广播的数据包接收。 在其中协议驱动程序，接收多路广播数据包的顺序并不重要。 有关详细信息，请参阅[OID\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)OID 请求。
-   设置数据包筛选器，包括**NDIS\_数据包\_类型\_所有\_多播**标记，可让所有的多路广播的数据包，并进行自身筛选。

微型端口驱动程序可以在数量的多播的地址列表可以包含的多播地址上设置限制。 返回 NDIS **NDIS\_状态\_多播\_完整**如果协议驱动程序超出此限制，或者指定了无效的多路广播的地址。

对于查询请求，NDIS 返回的所有协议绑定的所有多播的地址列表的并集的多路广播的地址列表。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_802\_3\_ADD\_MULTICAST\_ADDRESS](oid-802-3-add-multicast-address.md)

[OID\_802\_3\_DELETE\_MULTICAST\_ADDRESS](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_MAXIMUM\_LIST\_SIZE](oid-802-3-maximum-list-size.md)

[OID\_GEN\_CURRENT\_PACKET\_FILTER](oid-gen-current-packet-filter.md)

 

 




