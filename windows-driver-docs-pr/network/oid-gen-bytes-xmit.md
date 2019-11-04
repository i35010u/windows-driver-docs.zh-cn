---
title: OID_GEN_BYTES_XMIT
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_BYTES_XMIT OID 来确定微型端口适配器传输的总字节数。
ms.assetid: 95b89a01-39e0-4e13-b960-32923e47a88d
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_BYTES_XMIT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7ae58ebd9f7456278d14968911348aaf66294302
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73442986"
---
# <a name="oid_gen_bytes_xmit"></a>OID\_代\_字节\_XMIT


作为查询，NDIS 和过量驱动程序使用 OID\_代\_字节\_XMIT OID 来确定微型端口适配器传输的总字节数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 （请参见 "备注" 部分）

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的此 OID。 有关统计信息的详细信息，请参阅[OID\_GEN\_statistics](oid-gen-statistics.md) oid。

总字节数是传输传递的字节计数、传输多播字节计数和传输广播字节数的总和。 此值与 Oid\_GEN 返回的值的总和相同[\_定向\_字节\_XMIT](oid-gen-directed-bytes-xmit.md)， [oid\_代\_多播\_字节\_XMIT](oid-gen-multicast-bytes-xmit.md)和[OID\_代\_广播\_字节\_XMIT](oid-gen-broadcast-bytes-xmit.md) oid。

计数与 RFC 2863 中所述的*ifOutOctets*计数器完全相同。

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


[OID\_代\_广播\_字节\_XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID\_代\_定向\_字节\_XMIT](oid-gen-directed-bytes-xmit.md)

[OID\_代\_多播\_字节\_XMIT](oid-gen-multicast-bytes-xmit.md)

[OID\_代\_统计信息](oid-gen-statistics.md)

 

 




