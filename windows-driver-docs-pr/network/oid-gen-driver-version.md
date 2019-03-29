---
title: OID_GEN_DRIVER_VERSION
description: 为查询，OID_GEN_DRIVER_VERSION OID 指定 NDIS 版本的微型端口驱动程序在使用中。
ms.assetid: 8c3ac2ab-a83a-44d2-88bc-bd1468a0a59b
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_DRIVER_VERSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6ec8884119840a4f8af74f42663abb5368f54ff9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575624"
---
# <a name="oidgendriverversion"></a>OID\_GEN\_驱动程序\_版本


为查询，OID\_GEN\_驱动程序\_版本 OID 指定 NDIS 版本中使用的微型端口驱动程序。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

NDIS NDIS 6.0 和更高版本的微型端口驱动程序处理此 OID。

高字节是主版本号;低位字节是次版本号。

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

 

 




