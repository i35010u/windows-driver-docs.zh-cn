---
title: OID_GEN_DIRECTED_BYTES_RCV
description: 作为查询，OID_GEN_DIRECTED_BYTES_RCV OID 指定接收的数据包中的字节数，接收时不出现错误。
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_DIRECTED_BYTES_RCV 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b9aa9751a4c18ae4fa0390ce65d0d729a16b5823
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833335"
---
# <a name="oid_gen_directed_bytes_rcv"></a>OID \_ 生成 \_ 定向 \_ 字节 \_ RCV


作为查询，OID \_ GEN \_ 定向 \_ 字节 \_ RCV oid 指定接收的数据包中的字节数（接收时没有错误）。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
未请求。 请改用 [OID 生成 \_ \_ 统计信息](oid-gen-statistics.md) 。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a name="remarks"></a>备注
-------

计数与 RFC 2863 中所述的 *ifInUcastPkts* 计数器完全相同。

有关统计信息 Oid 的一般信息，请参阅 [常规统计](./ndis-general-statistics-oids.md)信息。

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


[OID \_ 生成 \_ 统计信息](oid-gen-statistics.md)

 

