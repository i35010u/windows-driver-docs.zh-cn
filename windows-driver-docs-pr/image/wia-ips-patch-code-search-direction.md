---
title: WIA\_IPS\_修补\_代码\_搜索\_方向
description: WIA\_IPS\_修补\_代码\_搜索\_方向属性用于配置 （相对于扫描方向） 的方向上每个扫描文档的修补程序代码在其中搜索设备页。
ms.assetid: 24541B0D-4B9B-439F-8454-AFDD3D16A448
keywords:
- WIA_IPS_PATCH_CODE_SEARCH_DIRECTION 成像设备
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
ms.openlocfilehash: 4a7a85ef48aeddb01938814acb7fdbd2ce1bc53e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366787"
---
# <a name="wiaipspatchcodesearchdirection"></a>WIA\_IPS\_修补\_代码\_搜索\_方向


**WIA\_IPS\_修补\_代码\_搜索\_方向**属性用于在其中配置 （相对于扫描方向） 的方向设备每个扫描文档页上的修补程序代码中搜索。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

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
<th>ReplTest1</th>
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
<td><p>设备搜索的修补程序代码首先水平然后垂直。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_VERTICAL_HORIZONTAL_SEARCH</p></td>
<td><p>设备搜索的修补程序代码首先垂直然后水平。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_AUTO_SEARCH</p></td>
<td><p>设备搜索中自动检测到在运行时或预定义其自身方向的修补程序代码。</p></td>
</tr>
</tbody>
</table>

 

此属性是必需的修补程序代码读取器的所有项，但它可以实现以支持仅 WIA\_修补程序\_代码\_自动\_搜索值。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





