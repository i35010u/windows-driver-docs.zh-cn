---
title: OID_GEN_MAX_LINK_SPEED
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_MAX_LINK_SPEED OID 来确定最大支持传输和接收的微型端口适配器链接速度。
ms.assetid: 4009c5c6-57ec-47f5-80d6-d69df797857f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAX_LINK_SPEED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bbfdbdb9d0dd747be6e650d2298e4aafa4f4d67b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358771"
---
# <a name="oidgenmaxlinkspeed"></a>OID\_GEN\_MAX\_LINK\_SPEED


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_最大\_链接\_速度 OID 来确定支持的最大传输和接收的微型端口适配器链接速度。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

微型端口驱动程序在初始化期间提供的最大链接速度。

若要指定最大链接速度，设置**MaxXmitLinkSpeed**并**MaxRcvLinkSpeed**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)微型端口驱动程序将传递给结构[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。 如果微型端口驱动程序不支持此 OID，则驱动程序应返回 NDIS\_状态\_不\_受支持。 如果微型端口驱动程序支持此 OID，它将返回中的最大链路速度[ **NDIS\_链接\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff565864)结构。

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


[**NDIS\_LINK\_SPEED**](https://msdn.microsoft.com/library/windows/hardware/ff565864)

[**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

 

 




