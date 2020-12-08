---
title: OID_GEN_BYTES_XMIT
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_BYTES_XMIT OID 来确定微型端口适配器传输的总字节数。
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_BYTES_XMIT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 43a75068ab0d6ef4fb9e38c3279b42635fb7a83f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806171"
---
# <a name="oid_gen_bytes_xmit"></a>OID \_ GEN \_ BYTES \_ XMIT


作为查询，NDIS 和过量驱动程序使用 OID \_ GEN \_ BYTES \_ XMIT oid 来确定微型端口适配器传输的总字节数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。  (参见 "备注" 部分) 

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的此 OID。 有关统计信息的详细信息，请参阅 [OID \_ GEN \_ STATISTICS](oid-gen-statistics.md) OID。

总字节数是传输传递的字节计数、传输多播字节计数和传输广播字节数的总和。 此值与 [oid \_ gen \_ 定向 \_ 字节 \_ XMIT](oid-gen-directed-bytes-xmit.md)、 [oid 生成 \_ \_ 多播 \_ 字节 \_ XMIT](oid-gen-multicast-bytes-xmit.md)和 [oid 生成 \_ \_ 广播 \_ 字节 \_ XMIT](oid-gen-broadcast-bytes-xmit.md) oid 返回的值的总和相同。

计数与 RFC 2863 中所述的 *ifOutOctets* 计数器完全相同。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ 生成 \_ 广播 \_ 字节 \_ XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID \_ 生成 \_ 定向 \_ 字节 \_ XMIT](oid-gen-directed-bytes-xmit.md)

[OID \_ 生成 \_ 多播 \_ 字节 \_ XMIT](oid-gen-multicast-bytes-xmit.md)

[OID \_ 生成 \_ 统计信息](oid-gen-statistics.md)

 

 




