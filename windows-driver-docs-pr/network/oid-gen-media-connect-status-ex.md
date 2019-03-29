---
title: OID_GEN_MEDIA_CONNECT_STATUS_EX
description: 为查询，OID_GEN_MEDIA_CONNECT_STATUS_EX OID 返回接口的连接状态。 Windows Vista 和 laterSupported。 NDIS 6.0 和更高版本的微型端口 driversNot 请求。 NDIS 接口提供程序仅。
ms.assetid: 8239616c-788a-4073-8bbe-41f493a461de
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_CONNECT_STATUS_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 340d83dee8f23949dd80e88e398dd92ee1a721cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575358"
---
# <a name="oidgenmediaconnectstatusex"></a>OID\_GEN\_媒体\_CONNECT\_状态\_EX


为查询，OID\_GEN\_媒体\_CONNECT\_状态\_EX OID 返回接口的连接状态。

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

NDIS 使用此 OID 来查询的连接状态[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566527)提供程序。 仅 NDIS 接口提供程序，并因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

如果查询成功，接口提供程序返回 NDIS\_状态\_成功和查询的结果可以是中的值之一[ **NET\_如果\_媒体\_CONNECT\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff568744)枚举。

微型端口驱动程序提供媒体在初始化过程中连接状态，并提供更新与状态的指示。

若要指定微型端口驱动程序中的连接状态，请设置**MediaConnectState**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)微型端口驱动程序将传递给结构[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

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


[**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[**NET\_IF\_媒体\_CONNECT\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff568744)

[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




