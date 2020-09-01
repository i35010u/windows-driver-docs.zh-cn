---
title: OID_GEN_MAXIMUM_SEND_PACKETS
description: 作为查询，OID_GEN_MAXIMUM_SEND_PACKETS OID 指定微型端口驱动程序的 MiniportSendPackets 函数可接受的发送数据包描述符的最大数目。
ms.assetid: 7e87285f-26c5-4b7d-99a8-bc0f30c643dc
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAXIMUM_SEND_PACKETS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ed7782e13269f413b38738ad3dc5100101286823
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210125"
---
# <a name="oid_gen_maximum_send_packets"></a>OID \_ 代 \_ 最大 \_ 发送 \_ 数据包


作为查询，OID \_ GEN \_ 最大 \_ 发送 \_ 数据包 OID 指定微型端口驱动程序的 [*MiniportSendPackets*](/previous-versions/windows/hardware/network/ff550524(v=vs.85)) 函数可接受的发送数据包描述符的最大数目。

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

NDIS 将忽略反序列化的驱动程序返回的任何值，以响应 OID \_ 代 \_ 最大 \_ 发送 \_ 数据包的查询。 NDIS 不会将其提供给反小端口驱动程序的 *MiniportSendPackets* 函数的数据包描述符数组的大小进行调整。

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

## <a name="see-also"></a>另请参阅


[*MiniportSendPackets*](/previous-versions/windows/hardware/network/ff550524(v=vs.85))

 

