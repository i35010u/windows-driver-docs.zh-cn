---
title: OID_802_3_MAXIMUM_LIST_SIZE
description: OID_802_3_MAXIMUM_LIST_SIZE
ms.assetid: e4288fb3-6bb3-415c-b150-1f258a2fa1a0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_802_3_MAXIMUM_LIST_SIZE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a2b7549db10514c21aff28c921ae079a5259761b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545563"
---
# <a name="oid8023maximumlistsize"></a>OID\_802\_3\_MAXIMUM\_LIST\_SIZE





NDIS 和基础协议驱动程序使用 OID\_802\_3\_最大\_列表\_大小 OID 请求来查询或设置最大数量的 6 个字节多播地址的微型端口适配器可容纳多路广播的地址列表。

由绑定到的微型端口适配器的所有协议驱动程序共享此多播的地址列表。 因为它是共享的资源，可以接收协议驱动程序**NDIS\_状态\_多播\_完整**从响应中的微型端口适配器[OID\_802\_3\_多播\_列表](oid-802-3-multicast-list.md)OID 设置请求，即使列表中的元素数小于 NDIS 以前返回的 OID 的数量\_802\_3\_最大\_列表\_大小 OID 查询请求。

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

[OID\_802\_3\_MULTICAST\_LIST](oid-802-3-multicast-list.md)

 

 




