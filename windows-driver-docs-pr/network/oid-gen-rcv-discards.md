---
title: OID_GEN_RCV_DISCARDS
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_RCV_DISCARDS OID 来确定接收数放弃微型端口适配器上。
ms.assetid: 638d2961-d327-490d-925b-3f6c30a13a89
ms.date: 08/08/2017
keywords: -OID_GEN_RCV_DISCARDS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 962c63cb3dc0a4d6f71260e80466de31e5fd5a1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367705"
---
# <a name="oidgenrcvdiscards"></a>OID\_GEN\_RCV\_放弃


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_RCV\_放弃 OID，若要确定接收数放弃微型端口适配器上。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 的微型端口驱动程序。 请参阅[OID\_代\_统计信息](oid-gen-statistics.md)OID 有关统计信息的详细信息。

计数是 RFC 2863 中所述的删除-接收-缓冲区错误计数。

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


[OID\_GEN\_STATISTICS](oid-gen-statistics.md)

 

 




