---
title: OID_GEN_RECEIVE_SCALE_CAPABILITIES
description: 作为查询，过量驱动程序可以使用 OID_GEN_RECEIVE_SCALE_CAPABILITIES OID 来查询 NIC 及其小型端口驱动程序 (RSS) 功能的接收方缩放。
ms.assetid: b7640ec3-248c-4db2-818d-3976df2dcb9b
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RECEIVE_SCALE_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 478644de4b4d4e52f4304244ba2b357ba2f6befa
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218375"
---
# <a name="oid_gen_receive_scale_capabilities"></a>OID \_ 生成 \_ 接收 \_ 缩放 \_ 功能


作为查询，过量驱动程序可以使用 OID 生成 \_ \_ 接收 \_ 缩放 \_ 功能 oid 查询接收方缩放 () NIC 的功能和其微型端口驱动程序。

<a name="remarks"></a>备注
-------

NDIS 微型端口驱动程序未收到此 OID 请求。 NDIS 处理微型端口驱动程序的查询。

微型端口驱动程序返回 [**NDIS \_ 接收 \_ 缩放 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities) 结构中的 RSS 功能。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 接收 \_ 缩放 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)

 

