---
title: 不需要进行任何更改的 WIA 属性映射
description: 不需要进行任何更改的 WIA 属性映射
ms.assetid: ceb0fe83-9803-4ba5-9a9f-7c722389db0b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 319052c912bc371b7742a1b88e0a91b9e8022621
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534422"
---
# <a name="mapping-wia-properties-that-need-no-changes"></a>不需要进行任何更改的 WIA 属性映射


没有具有相同的属性 Id 和属性名称与 Windows Vista 的 Windows XP 属性。 这些属性将转换与相应 Windows XP 上下文仅限选定内容;没有任何其他更改。 下面是这些 Windows XP 根属性以及它们在 Windows Vista 中将转换为的平板和送纸器 (ADF) 属性表。

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
<td><p><strong>Windows XP 项 / 上下文</strong></p></td>
<td><p><strong>Windows Vista 属性</strong></p></td>
<td><p><strong>Windows Vista</strong> <strong>项</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_CUR_INTENT</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_CUR_INTENT</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_CUR_INTENT</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_CUR_INTENT</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XRES</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_XRES</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XRES</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_XRES</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YRES</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_YRES</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YRES</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_YRES</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XPOS</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_XPOS</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XPOS</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_XPOS</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YPOS</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_YPOS</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YPOS</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_YPOS</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XEXTENT</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_XEXTENT</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XEXTENT</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_XEXTENT</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YEXTENT</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_YEXTENT</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YEXTENT</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_YEXTENT</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_CONTRAST</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_CONTRAST</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_CONTRAST</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_CONTRAST</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_ORIENTATION</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_ORIENTATION</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_ORIENTATION</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_ORIENTATION</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_ROTATION</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_ROTATION</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_ROTATION</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_ROTATION</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_THRESHOLD</p>
<p>读/写访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_THRESHOLD</p>
<p>读/写访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_THRESHOLD</p>
<p>读/写访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_THRESHOLD</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>只读访问权限</p></td>
<td><p>子 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>只读访问权限</p></td>
<td><p>子 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>请注意答：  
送纸器项 (ADF) 或 Windows XP 根或子项目上的送纸器上下文 (WIA\_DPS\_文档\_处理\_选择设置为送纸器)。

<a href="" id="note-b-"></a>请注意 b:  
平板项或 Windows XP 根或子项目上的平板上下文 (WIA\_DPS\_文档\_处理\_选择设置为平板)。

 

 




