---
title: WIA \_ IPS \_ 修补程序 \_ 代码 \_ 搜索 \_ 方向
description: "\"WIA \\_ IPS \\_ 修补程序 \\_ 代码 \\_ 搜索方向\" \\_ 属性用于配置相对于扫描方向 (方向，) 设备在每个扫描文档页面上搜索修补程序代码。"
keywords:
- WIA_IPS_PATCH_CODE_SEARCH_DIRECTION 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PATCH_CODE_SEARCH_DIRECTION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f90df639f11bb66f159373194ede1be0dfeb88d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804151"
---
# <a name="wia_ips_patch_code_search_direction"></a>WIA \_ IPS \_ 修补程序 \_ 代码 \_ 搜索 \_ 方向


" **WIA \_ IPS \_ 修补程序 \_ 代码 \_ 搜索 \_ 方向** " 属性用于配置相对于扫描方向 (方向，) 设备在每个扫描文档页面上搜索修补程序代码。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PATCH_CODE_HORIZONTAL_SEARCH</p></td>
<td><p>设备水平搜索修补程序代码。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_VERTICAL_SEARCH</p></td>
<td><p>设备垂直搜索修补程序代码。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_HORIZONTAL_VERTICAL_SEARCH</p></td>
<td><p>设备首先水平搜索修补程序代码。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_VERTICAL_HORIZONTAL_SEARCH</p></td>
<td><p>设备首先垂直和水平搜索修补程序代码。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_AUTO_SEARCH</p></td>
<td><p>设备会在运行时或预定义的自身方向搜索修补程序代码。</p></td>
</tr>
</tbody>
</table>

 

此属性是所有修补程序代码读取器项所必需的，但它可以实现为仅支持 WIA \_ 修补程序 \_ 代码 " \_ 自动 \_ 搜索" 值。

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





