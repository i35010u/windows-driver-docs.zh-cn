---
title: OID_GEN_VENDOR_ID
description: 为查询，OID_GEN_VENDOR_ID OID 指定三个字节 IEEE 注册供应商代码后, 跟一个字节的供应商用来标识特定的 nic。
ms.assetid: dce0a2e4-5d34-417f-9764-85644fe2ce46
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_VENDOR_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 21524157a2a2cb38f8c8b5b84f734b5ed2db16c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555603"
---
# <a name="oidgenvendorid"></a>OID\_GEN\_供应商\_ID


为查询，OID\_GEN\_供应商\_ID OID 指定三个字节 IEEE 注册供应商代码后, 跟一个字节的供应商用来标识特定的 nic。

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

IEEE 代码唯一标识供应商并等同于使其不显示在 NIC 硬件地址开头的三个字节。

未使用 IEEE 注册的代码的供应商应使用 0xFFFFFF 的值。

独立硬件供应商的筛选器驱动程序或中间驱动程序可以查询此 OID。

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

 

 




