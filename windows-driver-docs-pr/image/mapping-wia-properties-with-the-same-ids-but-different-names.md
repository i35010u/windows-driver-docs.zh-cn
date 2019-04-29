---
title: 映射 ID 相同但名称不同的 WIA 属性
description: 映射 ID 相同但名称不同的 WIA 属性
ms.assetid: 0321db59-74a1-4294-bbaf-ec0b9317464b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12b5e4b21bc58c97c2e04130ceb3181e6f0719f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380361"
---
# <a name="mapping-wia-properties-with-the-same-ids-but-different-names"></a>映射 ID 相同但名称不同的 WIA 属性


没有具有相同的属性 Id 与 Windows Vista 的对应不同的属性名称，但 Windows XP 属性。 下面是这些 Windows XP 根属性以及它们在 Windows Vista 中将转换为的平板和送纸器 (ADF) 属性表。

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
<p><strong>项 / 上下文</strong></p></td>
<td><p><strong>Windows Vista 属性</strong></p></td>
<td><p><strong>Windows Vista</strong> <strong>项</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_DOCUMENT_HANDLING_SELECT</p>
<p>读/写访问，请参阅备注： d</p></td>
<td><p>根</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_IPS_DOCUMENT_HANDLING_SELECT</p>
<p>读/写访问，请参阅备注： d</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_SHEET_FEEDER_REGISTRATION</p>
<p>只读访问权限</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_SHEET_FEEDER_REGISTRATION</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_OPTICAL_XRES</p>
<p>只读访问权限</p></td>
<td><p>根 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_OPTICAL_XRES</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_OPTICAL_XRES</p>
<p>只读访问权限</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_OPTICAL_XRES</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_OPTICAL_YRES</p>
<p>只读访问权限</p></td>
<td><p>根 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_OPTICAL_YRES</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_OPTICAL_YRES</p>
<p>只读访问权限</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_OPTICAL_YRES</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PAGES</p>
<p>读/写访问权限</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_PAGES</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PAGE_SIZE</p>
<p>读/写访问权限，请参阅注意： e</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_PAGE_SIZE</p>
<p>读/写访问权限，请参阅注意： e</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PAGE_WIDTH</p>
<p>只读访问权限</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_PAGE_WIDTH</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PAGE_HEIGHT</p>
<p>只读访问权限</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_PAGE_WIDTH</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PREVIEW</p>
<p>读/写访问权限</p></td>
<td><p>根 / 平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_PREVIEW</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PREVIEW</p>
<p>读/写访问权限</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_PREVIEW</p>
<p>读/写访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_SHOW_PREVIEW_CONTROL</p>
<p>只读访问权限</p></td>
<td><p>根 / 平板</p>
<p>请参阅备注： c</p></td>
<td><p>WIA_IPS_SHOW_PREVIEW_CONTROL</p>
<p>只读访问权限</p></td>
<td><p>平板</p>
<p>请参阅备注： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_SHOW_PREVIEW_CONTROL</p>
<p>只读访问权限</p></td>
<td><p>根 / 送纸器</p>
<p>请参阅注释：</p></td>
<td><p>WIA_IPS_SHOW_PREVIEW_CONTROL</p>
<p>只读访问权限</p></td>
<td><p>送纸器</p>
<p>请参阅注释：</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>请注意答：  
送纸器项 (ADF) 或 Windows XP 根或子项目上的送纸器上下文 (WIA\_DPS\_文档\_处理\_选择设置为送纸器)

<a href="" id="note-b-"></a>请注意 b:  
平板项或 Windows XP 根或子项目上的平板上下文 (WIA\_DPS\_文档\_处理\_选择设置为平板)

<a href="" id="note-c-"></a>请注意 c:  
根项，指定适用于 Windows XP 没有上下文

<a href="" id="note-d-"></a>请注意 d:  
适用于 Windows XP 到 Windows Vista 的转换：

返回\_第一个

返回\_仅

双工

前端\_第一个

前端\_仅

前端\_仅是默认值，如果未实现此属性。

请注意 e:所有值，而不仅仅是旧的都转换 (WIA\_页上\_自定义、 WIA\_页面\_A4、 WIA\_页\_字母)

请注意，必须为相应的平板/送纸器上下文组配置 Windows XP 根项 (通过 WIA\_DPS\_文档\_处理\_选择) 之前访问 （两者都依赖于上下文的属性用于读取和写入访问）。

 

 




