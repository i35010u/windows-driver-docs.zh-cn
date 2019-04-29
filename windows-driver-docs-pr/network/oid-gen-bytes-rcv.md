---
title: OID_GEN_BYTES_RCV
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_BYTES_RCV OID 来确定的微型端口适配器接收的字节总数。
ms.assetid: e613e155-e4ff-48e4-8087-20ecad3c4644
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_BYTES_RCV 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8bc492c7c2a3605925401dbc0cb0b16a375a1f96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323582"
---
# <a name="oidgenbytesrcv"></a>OID\_GEN\_BYTES\_RCV


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_字节\_RCV OID 来确定的微型端口适配器接收的字节总数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 的微型端口驱动程序。 请参阅[OID\_代\_统计信息](oid-gen-statistics.md)OID 有关统计信息的详细信息。

总字节数是定向接收的字节数、 接收多播字节数和接收广播字节数的总和。 此值等同于返回的值的总和[OID\_代\_定向\_字节\_RCV](oid-gen-directed-bytes-rcv.md)， [OID\_常规\_多播\_字节\_RCV](oid-gen-multicast-bytes-rcv.md)，和[OID\_常规\_广播\_字节\_RCV](oid-gen-broadcast-bytes-rcv.md) Oid。

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


[OID\_GEN\_BROADCAST\_BYTES\_RCV](oid-gen-broadcast-bytes-rcv.md)

[OID\_GEN\_DIRECTED\_BYTES\_RCV](oid-gen-directed-bytes-rcv.md)

[OID\_GEN\_MULTICAST\_BYTES\_RCV](oid-gen-multicast-bytes-rcv.md)

[OID\_GEN\_STATISTICS](oid-gen-statistics.md)

 

 




