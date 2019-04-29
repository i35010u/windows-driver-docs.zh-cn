---
title: OID_GEN_MAXIMUM_SEND_PACKETS
description: 为查询，OID_GEN_MAXIMUM_SEND_PACKETS OID 指定发送包描述符的微型端口驱动程序的 MiniportSendPackets 函数可以接受的最大数目。
ms.assetid: 7e87285f-26c5-4b7d-99a8-bc0f30c643dc
ms.date: 08/08/2017
keywords: -OID_GEN_MAXIMUM_SEND_PACKETS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4a9b2b2828bae1cabfd19ba17f7a9748bdcd605b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358755"
---
# <a name="oidgenmaximumsendpackets"></a>OID\_GEN\_最大\_发送\_数据包


为查询，OID\_GEN\_最大\_发送\_数据包 OID 指定的最大数目发送的数据包描述符微型端口驱动程序[ *MiniportSendPackets*](https://msdn.microsoft.com/library/windows/hardware/ff550524)函数可以接受。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
已过时。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

NDIS 忽略返回 OID 的查询响应中的反序列化驱动程序的任何值\_GEN\_最大\_发送\_数据包。 NDIS 不调整它提供给反序列化的微型端口驱动程序的数据包描述符的数组的大小*MiniportSendPackets*函数。

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


[*MiniportSendPackets*](https://msdn.microsoft.com/library/windows/hardware/ff550524)

 

 




