---
title: OID_GEN_BYTES_RCV
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_BYTES_RCV OID 来确定微型端口适配器接收到的总字节数。
ms.assetid: e613e155-e4ff-48e4-8087-20ecad3c4644
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_BYTES_RCV 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0df977f94e4ae3fd7ce85f45609f0049322bc6cc
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443006"
---
# <a name="oid_gen_bytes_rcv"></a>OID\_代\_字节\_RCV


作为查询，NDIS 和过量驱动程序使用 OID\_代\_字节\_RCV OID 来确定微型端口适配器接收到的总字节数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 （请参见 "备注" 部分）

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的此 OID。 有关统计信息的详细信息，请参阅[OID\_GEN\_statistics](oid-gen-statistics.md) oid。

总字节数是接收定向字节计数、接收-多播字节计数和接收广播字节数的总和。 此值与 Oid\_GEN 返回的值的总和相同[\_定向\_字节\_RCV](oid-gen-directed-bytes-rcv.md)， [oid\_代\_多播\_字节\_RCV](oid-gen-multicast-bytes-rcv.md)和[OID\_代\_广播\_字节\_RCV](oid-gen-broadcast-bytes-rcv.md) oid。

计数与 RFC 2863 中所述的*ifInOctets*计数器完全相同。

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


[OID\_代\_广播\_字节\_RCV](oid-gen-broadcast-bytes-rcv.md)

[OID\_代\_定向\_字节\_RCV](oid-gen-directed-bytes-rcv.md)

[OID\_代\_多播\_字节\_RCV](oid-gen-multicast-bytes-rcv.md)

[OID\_代\_统计信息](oid-gen-statistics.md)

 

 




