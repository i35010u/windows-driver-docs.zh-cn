---
title: OID_GEN_XMIT_DISCARDS
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_XMIT_DISCARDS OID 来确定传输数放弃微型端口适配器上。
ms.assetid: f6265262-c485-441c-bb89-fa1d302608d2
ms.date: 08/08/2017
keywords: -OID_GEN_XMIT_DISCARDS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5e28c7d4ca38bb09a9ee8ca6c517bc3ddbc12bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354183"
---
# <a name="oidgenxmitdiscards"></a>OID\_GEN\_XMIT\_放弃


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_XMIT\_放弃 OID，若要确定传输数放弃微型端口适配器上。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 的微型端口驱动程序。 请参阅[OID\_代\_统计信息](oid-gen-statistics.md)OID 有关统计信息的详细信息。

此 OID 返回的计数是由接口将被丢弃的数据包数。

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

 

 




