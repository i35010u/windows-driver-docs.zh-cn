---
title: OID_GEN_MEDIA_IN_USE
description: 为查询，OID_GEN_MEDIA_IN_USE OID 指定 NIC 当前使用的媒体类型的完整列表。
ms.assetid: 3b8db63d-07e0-4a5c-9848-57e594e3dd54
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_IN_USE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 09b3af88cf9cb83c88ba9acd94721ee4bd242c10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348147"
---
# <a name="oidgenmediainuse"></a>OID\_GEN\_MEDIA\_IN\_USE


为查询，OID\_GEN\_媒体\_IN\_使用 OID 指定 NIC 当前使用的媒体类型的完整列表。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

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

NDIS 6.0 和更高版本的微型端口驱动程序不会收到此 OID 请求。 NDIS 处理此 OID 微型端口驱动程序在初始化过程中提供的缓存值。

此 OID 提供相同的信息[OID\_代\_媒体\_支持](oid-gen-media-supported.md)OID。

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


[OID\_GEN\_媒体\_支持](oid-gen-media-supported.md)

 

 




