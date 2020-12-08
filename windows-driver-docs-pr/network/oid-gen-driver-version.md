---
title: OID_GEN_DRIVER_VERSION
description: 作为查询，OID_GEN_DRIVER_VERSION OID 指定微型端口驱动程序使用的 NDIS 版本。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_DRIVER_VERSION 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fd2f6ef9192106dc67c2ab01290b2cc1e11dd803
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789661"
---
# <a name="oid_gen_driver_version"></a>OID \_ 生成 \_ 驱动程序 \_ 版本


作为查询，OID 生成 \_ \_ 驱动程序 \_ 版本 oid 指定微型端口驱动程序使用的 NDIS 版本。

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

NDIS 处理 NDIS 6.0 和更高版本的小型小型驱动程序的此 OID。

高字节是主版本号;低字节是次版本号。

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

 

 




