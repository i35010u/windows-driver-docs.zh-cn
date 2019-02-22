---
title: OID_GEN_LINK_SPEED_EX
description: 为查询，OID_GEN_LINK_SPEED_EX OID 提供了传输和接收链接速度的接口。 版本信息 Windows Vista 和 laterSupported。 NDIS 6.0 和更高版本的微型端口 driversNot 请求。 NDIS 接口提供程序仅。
ms.assetid: 86cc281b-3898-484c-9418-4408a45ebe71
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_SPEED_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a24c28d3dccef45e726e29d0c68212effbb33963
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554747"
---
# <a name="oidgenlinkspeedex"></a>OID\_GEN\_LINK\_SPEED\_EX


为查询，OID\_GEN\_链接\_速度\_EX OID 提供了传输和接收链接速度的接口。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

NDIS 使用此 OID 来查询的链接速度[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566527)提供程序。 仅 NDIS 接口提供程序，并因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

此 OID 返回中的链接速度[ **NDIS\_链接\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff565864)结构。

微型端口驱动程序在初始化过程中提供的链接速度，并提供状态指示已更新的链接速度。

若要指定链接速度微型端口驱动程序中，设置**XmitLinkSpeed**并**RcvLinkSpeed**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)微型端口驱动程序将传递给结构[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_LINK\_SPEED**](https://msdn.microsoft.com/library/windows/hardware/ff565864)

[**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




