---
title: WIA\_IPS\_支持\_修补\_代码\_类型
description: WIA 微型驱动程序使用 WIA\_IPS\_支持\_修补\_代码\_类型属性可以列出 （理解） 的修补程序代码读取器支持的所有修补程序代码类型。
ms.assetid: DA55BFFD-64E9-4D96-AB04-F2112E1F117B
keywords:
- WIA_IPS_SUPPORTED_PATCH_CODE_TYPES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SUPPORTED_PATCH_CODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c47b9810313db00796afbfacca7d5a353d1838d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343835"
---
# <a name="wiaipssupportedpatchcodetypes"></a>WIA\_IPS\_支持\_修补\_代码\_类型


使用 WIA 微型驱动程序**WIA\_IP\_支持\_修补\_代码\_类型**属性可以列出 （理解） 的修补程序支持的所有修补程序代码类型代码读取器。 受支持的条形码类型报告中 VT\_向量数组作为单个值，该值包含多个条目。




属性类型：VT\_I4 | VT\_VECTOR

有效值：WIA\_PROP\_NONE （单一 array / 矢量值）

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_支持\_修补\_代码\_类型**属性。

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
<td><p>WIA_PATCH_CODE_1</p></td>
<td><p>修补程序代码 1</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_2</p></td>
<td><p>修补程序代码 2</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_3</p></td>
<td><p>修补程序代码 3</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_4</p></td>
<td><p>修补程序代码 4</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_6</p></td>
<td><p>修补程序代码 6</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_T</p></td>
<td><p>修补程序代码 T</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_CUSTOM_BASE + N</p></td>
<td><p>WIA_PATCH_CODE_CUSTOM_BASE 是到 WIA 微型驱动程序可能添加的所有自定义修补程序代码值的偏移量。 N 是一个正整数。</p></td>
</tr>
</tbody>
</table>

 

WIA 微型驱动程序可以使用定义为 WIA 的其他自定义值来扩展此列表\_修补\_代码\_自定义\_基本 + N，其中 N 是一个正整数。

此属性是必需的修补程序代码读取器的所有项。

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

 

 





