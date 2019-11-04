---
title: OID_GEN_XMIT_DISCARDS
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_XMIT_DISCARDS OID 来确定微型端口适配器上丢弃的传输数。
ms.assetid: f6265262-c485-441c-bb89-fa1d302608d2
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_XMIT_DISCARDS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8ec55f499e3c1e0b88ebfaf4d4d1ddb3a24ae951
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443050"
---
# <a name="oid_gen_xmit_discards"></a>OID\_代\_XMIT\_放弃


作为查询，NDIS 和过量驱动程序使用 OID\_GEN\_XMIT\_放弃 OID，以确定微型端口适配器上丢弃的传输数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 （请参见 "备注" 部分）

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的此 OID。 有关统计信息的详细信息，请参阅[OID\_GEN\_statistics](oid-gen-statistics.md) oid。

此 OID 返回的计数是接口丢弃的数据包数。 计数与 RFC 2863 中所述的*ifOutDiscards*计数器完全相同。

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


[OID\_代\_统计信息](oid-gen-statistics.md)

 

 




