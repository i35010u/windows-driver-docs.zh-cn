---
title: OID_GEN_BYTES_XMIT
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_BYTES_XMIT OID 来确定微型端口适配器传输的总字节数。
ms.assetid: 95b89a01-39e0-4e13-b960-32923e47a88d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_BYTES_XMIT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 23f59d11ee505a0477b08f1172fdc393df6c6635
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565140"
---
# <a name="oidgenbytesxmit"></a>OID\_GEN\_字节\_XMIT


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_字节\_XMIT OID，以确定微型端口适配器传输的总字节数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 的微型端口驱动程序。 请参阅[OID\_代\_统计信息](oid-gen-statistics.md)OID 有关统计信息的详细信息。

总字节数是定向传输的字节数、 传输多播字节数和传输广播字节数的总和。 此值等同于返回的值的总和[OID\_代\_定向\_字节\_XMIT](oid-gen-directed-bytes-xmit.md)， [OID\_常规\_多播\_字节\_XMIT](oid-gen-multicast-bytes-xmit.md)，和[OID\_常规\_广播\_字节\_XMIT](oid-gen-broadcast-bytes-xmit.md) Oid。

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


[OID\_GEN\_BROADCAST\_BYTES\_XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID\_GEN\_DIRECTED\_BYTES\_XMIT](oid-gen-directed-bytes-xmit.md)

[OID\_GEN\_MULTICAST\_BYTES\_XMIT](oid-gen-multicast-bytes-xmit.md)

[OID\_GEN\_STATISTICS](oid-gen-statistics.md)

 

 




