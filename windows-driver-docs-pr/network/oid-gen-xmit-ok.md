---
title: OID_GEN_XMIT_OK
description: 为查询，OID_GEN_XMIT_OK OID 指定没有错误传输的帧数。
ms.assetid: ac7120a3-58bb-4047-b4b7-ad9fbaf14e4f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_XMIT_OK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d97a14765112a61347797a6283dd6f5431c492b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385734"
---
# <a name="oidgenxmitok"></a>OID\_GEN\_XMIT\_确定


为查询，OID\_GEN\_XMIT\_确定 OID 指定没有错误传输的帧数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本的驱动程序  
必需。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a name="remarks"></a>备注
-------

OID\_GEN\_XMIT\_确定指定的错误没有传输的帧数。 但是， [OID\_代\_统计信息](oid-gen-statistics.md)不包括此信息。

注意：统计信息 Oid 是强制性的 NDIS 6.0 和更高版本的微型端口驱动程序，除非 NDIS 处理它们。 有关 Oid 的统计信息的常规信息，请参阅[General Statistics](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)。

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

 

 




