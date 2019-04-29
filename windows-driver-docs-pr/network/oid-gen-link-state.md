---
title: OID_GEN_LINK_STATE
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_LINK_STATE OID 来确定微型端口适配器的当前链接状态。
ms.assetid: 75a30054-8700-4b79-902c-c8382a25c0a2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7b37225cde129644fba488a88aa4d51d480fa511
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358889"
---
# <a name="oidgenlinkstate"></a>OID\_GEN\_链接\_状态


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_链接\_状态 OID，以确定微型端口适配器的当前链接状态。 微型端口驱动程序接收中的链接状态[ **NDIS\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh205390)结构。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

微型端口驱动程序在初始化过程中提供的链接状态，并提供更新与状态的指示。

若要指定链接状态，请设置**MediaConnectState**， **MediaDuplexState**， **XmitLinkSpeed**， **RcvLinkSpeed**， **PauseFunctions**，并**AutoNegotiationFlags**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构的微型端口驱动程序将传递给[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

如果微型端口驱动程序不支持此 OID，则驱动程序应返回 NDIS\_状态\_不\_受支持。 如果微型端口驱动程序支持此 OID，它将返回的连接状态、 双工状态，并链接速度中[ **NDIS\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh205390)结构。

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


[**NDIS\_LINK\_STATE**](https://msdn.microsoft.com/library/windows/hardware/hh205390)

[**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[OID\_GEN\_媒体\_CONNECT\_状态\_EX](oid-gen-media-connect-status-ex.md)

[OID\_GEN\_MEDIA\_DUPLEX\_STATE](oid-gen-media-duplex-state.md)

 

 




