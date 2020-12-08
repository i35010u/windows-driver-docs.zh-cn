---
title: OID_GEN_MEDIA_IN_USE
description: 作为查询，OID_GEN_MEDIA_IN_USE OID 指定了 NIC 当前使用的媒体类型的完整列表。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_IN_USE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 997836f8f1f4e75d69025f094d78dc5288b2dc2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792651"
---
# <a name="oid_gen_media_in_use"></a>\_ \_ \_ 正在 \_ 使用 OID 生成媒体


作为查询，OID \_ 代 \_ 媒体 \_ \_ 使用 oid 指定了 NIC 当前使用的媒体类型的完整列表。

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

NDIS 6.0 和更高版本的微型端口驱动程序不会收到此 OID 请求。 NDIS 使用小型端口驱动程序在初始化期间提供的缓存值处理此 OID。

此 OID 提供与 [oid 生成 \_ \_ 媒体 \_ 支持](oid-gen-media-supported.md) 的 oid 相同的信息。

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

## <a name="see-also"></a>请参阅


[支持 OID 生成 \_ \_ 媒体 \_](oid-gen-media-supported.md)

 

 




