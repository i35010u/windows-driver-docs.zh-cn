---
title: 映射不需更改的 WIA 属性
description: 映射不需更改的 WIA 属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50c92457f55f9f46ed506081da642f1714ef3530
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796181"
---
# <a name="mapping-wia-properties-that-need-no-changes"></a>映射不需更改的 WIA 属性


存在与 Windows Vista 对应项具有相同属性 Id 和属性名称的 Windows XP 属性。 仅通过适当的 Windows XP 上下文选择转换这些属性;没有其他更改。 下面是在 Windows Vista 中将其转换为的 Windows XP 根属性和平板和进纸器 (ADF) 属性的表格。

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
<td><p><strong>Windows XP 项/上下文</strong></p></td>
<td><p><strong>Windows Vista 属性</strong></p></td>
<td><p><strong>Windows Vista</strong> <strong>项</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_CUR_INTENT</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_CUR_INTENT</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_CUR_INTENT</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_CUR_INTENT</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XRES</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_XRES</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XRES</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_XRES</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YRES</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_YRES</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YRES</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_YRES</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XPOS</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_XPOS</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XPOS</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_XPOS</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YPOS</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_YPOS</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YPOS</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_YPOS</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XEXTENT</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_XEXTENT</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XEXTENT</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_XEXTENT</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YEXTENT</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_YEXTENT</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YEXTENT</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_YEXTENT</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_CONTRAST</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_CONTRAST</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_CONTRAST</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_CONTRAST</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_ORIENTATION</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_ORIENTATION</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_ORIENTATION</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_ORIENTATION</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_ROTATION</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_ROTATION</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_ROTATION</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_ROTATION</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_THRESHOLD</p>
<p>读/写访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_THRESHOLD</p>
<p>读/写访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_THRESHOLD</p>
<p>读/写访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_THRESHOLD</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>只读访问</p></td>
<td><p>子/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>只读访问</p></td>
<td><p>子/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>注意 a：  
在 Windows XP 根项或子项 (WIA DPS 文档处理中， (ADF) 或进纸器上下文的进纸器项 \_ \_ \_ \_ 设置为 "馈送器) "。

<a href="" id="note-b-"></a>备注 b：  
Windows XP 根或子项目上的平板物品或平板上下文 (WIA \_ DPS \_ 文档 \_ 处理 \_ 选择设置为平板) 。

 

 




