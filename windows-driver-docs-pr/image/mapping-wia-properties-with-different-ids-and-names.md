---
title: 映射具有不同 ID 和名称的 WIA 属性
description: 映射具有不同 ID 和名称的 WIA 属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e103f50c6db11e6237388354c19c4c3c0750eab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803861"
---
# <a name="mapping-wia-properties-with-different-ids-and-names"></a>映射具有不同 ID 和名称的 WIA 属性


有一些 Windows XP 属性，这些属性的属性 Id 和 Windows Vista 中的属性名称不同。 下面是在 Windows Vista 中将其转换为的 Windows XP 根属性和平板和进纸器 (ADF) 属性的表格。

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
<p><strong>项/上下文</strong></p></td>
<td><p><strong>Windows Vista 属性</strong></p></td>
<td><p><strong>Windows Vista</strong> <strong>项</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_HORIZONTAL_BED_SIZE</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_VERTICAL_BED_SIZE</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_MAX_VERTICAL_SIZE</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_HORIZONTAL_SHEET_FEED_SIZE</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_VERTICAL_SHEET_FEED_SIZE</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_MIN_HORIZONTAL_SHEET_FEED_SIZE</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_MIN_HORIZONTAL_SIZE</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_MIN_VERTICAL_SHEET_FEED_SIZE</p>
<p>只读访问</p></td>
<td><p>Root</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_MIN_VERTICAL_SIZE</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="even">
<td><p>一般值：1</p></td>
<td><p>NA</p></td>
<td><p>WIA_IPS_MIN_HORIZONTAL_SIZE</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="odd">
<td><p>一般值：1</p></td>
<td><p>NA</p></td>
<td><p>WIA_IPS_MIN_VERTICAL_SIZE</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅注意： c</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>注意 a：  
根项，未指定用于 Windows XP 的上下文

<a href="" id="note-b-"></a>备注 b：  
Windows XP root 或 child 项上的平板物品或平板上下文 (WIA \_ DPS \_ 文档 \_ 处理 \_ 选择设置为平板) 

<a href="" id="note-c-"></a>备注 c：  
 (ADF) 上的进纸器项、Windows XP 根项或子项目上的进纸器上下文 (WIA \_ DPS \_ 文档 \_ 处理 \_ 选择已设置为送) 送

 

 




