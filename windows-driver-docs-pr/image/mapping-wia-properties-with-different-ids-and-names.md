---
title: 映射具有不同 ID 和名称的 WIA 属性
description: 映射具有不同 ID 和名称的 WIA 属性
ms.assetid: e3a352fc-c817-466e-bd04-0ec8b029d500
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6373f74f0fb71a04845a2d73678bc10935f8106
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380375"
---
# <a name="mapping-wia-properties-with-different-ids-and-names"></a>映射具有不同 ID 和名称的 WIA 属性


没有具有不同的属性 Id 和不同的属性名称从对应的 Windows Vista 的 Windows XP 属性。 下面是这些 Windows XP 根属性以及它们在 Windows Vista 中将转换为的平板和送纸器 (ADF) 属性表。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows XP 属性</strong></p></td>
<td><p><strong>Windows XP</strong></p>
<p><strong>item/context</strong></p></td>
<td><p><strong>Windows Vista 属性</strong></p></td>
<td><p><strong>Windows Vista</strong> <strong>项</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_HORIZONTAL_BED_SIZE</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_VERTICAL_BED_SIZE</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_MAX_VERTICAL_SIZE</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_HORIZONTAL_SHEET_FEED_SIZE</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_VERTICAL_SHEET_FEED_SIZE</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_MIN_HORIZONTAL_SHEET_FEED_SIZE</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_MIN_HORIZONTAL_SIZE</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_MIN_VERTICAL_SHEET_FEED_SIZE</p>
<p>只读访问权限</p></td>
<td><p>根</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_MIN_VERTICAL_SIZE</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="even">
<td><p>泛型值：1</p></td>
<td><p>NA</p></td>
<td><p>WIA_IPS_MIN_HORIZONTAL_SIZE</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="odd">
<td><p>泛型值：1</p></td>
<td><p>NA</p></td>
<td><p>WIA_IPS_MIN_VERTICAL_SIZE</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： c</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>请注意答：  
根项，指定适用于 Windows XP 没有上下文

<a href="" id="note-b-"></a>请注意 b:  
平板项或 Windows XP 根或子项目上的平板上下文 (WIA\_DPS\_文档\_处理\_选择设置为平板)

<a href="" id="note-c-"></a>请注意 c:  
送纸器项 (ADF) 或 Windows XP 根或子项目上的送纸器上下文 (WIA\_DPS\_文档\_处理\_选择设置为送纸器)

 

 




