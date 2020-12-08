---
title: WIA \_ IP \_ 支持的 \_ 修补程序 \_ 代码 \_ 类型
description: WIA 微型驱动程序使用 "WIA \_ IPS \_ 支持的 \_ 修补程序 \_ 代码类型" \_ 属性列出修补程序代码读取器所支持 () 理解的所有修补程序代码类型。
keywords:
- WIA_IPS_SUPPORTED_PATCH_CODE_TYPES 图像设备
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
ms.openlocfilehash: 2a55dbc1874afe603bde046efe80d42b2eb383dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814419"
---
# <a name="wia_ips_supported_patch_code_types"></a>WIA \_ IP \_ 支持的 \_ 修补程序 \_ 代码 \_ 类型


WIA 微型驱动程序使用 " **wia \_ IPS 支持 \_ 的 \_ 修补程序 \_ 代码 \_ 类型** " 属性列出修补程序代码读取器所支持 () 理解的所有修补程序代码类型。 支持的条码类型在 VT \_ 矢量数组中报告为包含多个条目的单个值。




属性类型： VT \_ I4 |VT \_ 矢量

有效值： WIA \_ \_ (单个 "array"/vector 值) 

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ IPS \_ 支持的 \_ 修补程序 \_ 代码 \_ 类型** " 属性的有效值。

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
<td><p>WIA_PATCH_CODE_1</p></td>
<td><p>修补程序代码1</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_2</p></td>
<td><p>修补程序代码2</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_3</p></td>
<td><p>修补程序代码3</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_4</p></td>
<td><p>修补程序代码4</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_6</p></td>
<td><p>修补程序代码6</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_T</p></td>
<td><p>修补程序代码 T</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_CUSTOM_BASE + N</p></td>
<td><p>WIA_PATCH_CODE_CUSTOM_BASE 是 WIA 微型驱动程序可以添加的所有自定义修补程序代码值的偏移量。 N 是一个正整数。</p></td>
</tr>
</tbody>
</table>

 

WIA 微型驱动程序可以使用定义为 WIA \_ 修补程序代码自定义基数 + N 的附加自定义值扩展此列表 \_ \_ \_ ，其中 N 是一个正整数。

所有修补程序代码读取器项都需要此属性。

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

 

 





