---
title: OID_GEN_MINIPORT_RESTART_ATTRIBUTES
description: OID_GEN_MINIPORT_RESTART_ATTRIBUTES OID 标识的 NDIS 驱动程序堆栈中的微型端口适配器重启属性传播的常规属性。
ms.assetid: 239993f6-2176-4925-aadc-44e0df66f56b
ms.date: 08/08/2017
keywords: -OID_GEN_MINIPORT_RESTART_ATTRIBUTES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2cb128805f2e0c682bfda9307d64cf357d77efcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348119"
---
# <a name="oidgenminiportrestartattributes"></a>OID\_GEN\_微型端口\_重新启动\_属性


OID\_GEN\_微型端口\_重新启动\_属性 OID 标识的 NDIS 驱动程序堆栈中的微型端口适配器重启属性传播的常规属性。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a name="remarks"></a>备注
-------

OID\_GEN\_微型端口\_重新启动\_属性 OID 不用于发出 OID 查询或设置请求。

如果**Oid**中的成员[ **NDIS\_重新启动\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)结构是 OID\_常规\_微型端口\_重新启动\_属性，**数据**结构中的成员包含[ **NDIS\_重新启动\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567260)结构。

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


[**NDIS\_重新启动\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)

[**NDIS\_RESTART\_GENERAL\_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff567260)

 

 




