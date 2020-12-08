---
title: OID_GEN_VENDOR_ID
description: 作为查询，OID_GEN_VENDOR_ID OID 指定三字节 IEEE 注册供应商代码，后跟供应商分配的单个字节来识别特定的 NIC。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_VENDOR_ID 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: eb34849b121f3e66a9a773162289850882b39bc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782217"
---
# <a name="oid_gen_vendor_id"></a>OID \_ 生成 \_ 供应商 \_ ID


作为查询，OID 生成 \_ \_ 供应商 \_ ID OID 指定三字节 IEEE 注册供应商代码，后跟供应商分配用于标识特定 NIC 的单个字节。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

IEEE 代码唯一地标识供应商，与显示在 NIC 硬件地址开头的三个字节相同。

没有 IEEE 注册代码的供应商应该使用值0xFFFFFF。

独立硬件供应商的筛选器驱动程序或中间驱动程序可能会查询此 OID。

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

 

 




