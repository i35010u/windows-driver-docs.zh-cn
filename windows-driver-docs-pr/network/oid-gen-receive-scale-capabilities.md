---
title: OID_GEN_RECEIVE_SCALE_CAPABILITIES
description: 作为查询，过量驱动程序可以使用 OID_GEN_RECEIVE_SCALE_CAPABILITIES OID 来查询 NIC 及其小型端口驱动程序的接收方缩放（RSS）功能。
ms.assetid: b7640ec3-248c-4db2-818d-3976df2dcb9b
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_SCALE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 71c7dd1837db03e419f048c01549775854b481d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840475"
---
# <a name="oid_gen_receive_scale_capabilities"></a>OID\_代\_接收\_扩展\_功能


作为查询，过量驱动程序可以使用 OID\_GEN\_接收\_扩展\_功能 OID，以查询 NIC 及其小型端口驱动程序的接收方缩放（RSS）功能。

<a name="remarks"></a>备注
-------

NDIS 微型端口驱动程序未收到此 OID 请求。 NDIS 处理微型端口驱动程序的查询。

微型端口驱动程序返回 NDIS 中的 RSS 功能[ **\_接收\_缩放\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)结构。

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
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_接收\_缩放\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)

 

 




