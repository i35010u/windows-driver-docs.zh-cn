---
title: 映射 ID 相同但名称不同的 WIA 属性
description: 映射 ID 相同但名称不同的 WIA 属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7793594f2cdd935318f73413d19c62a1a4074627
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816233"
---
# <a name="mapping-wia-properties-with-the-same-ids-but-different-names"></a>映射 ID 相同但名称不同的 WIA 属性


Windows XP 属性具有相同的属性 Id 但不同于 Windows Vista 的属性名称。 下面是在 Windows Vista 中将其转换为的 Windows XP 根属性和平板和进纸器 (ADF) 属性的表格。

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
<td><p>WIA_DPS_DOCUMENT_HANDLING_SELECT</p>
<p>读/写访问权限，请参阅： d</p></td>
<td><p>Root</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_IPS_DOCUMENT_HANDLING_SELECT</p>
<p>读/写访问权限，请参阅： d</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_SHEET_FEEDER_REGISTRATION</p>
<p>只读访问</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_SHEET_FEEDER_REGISTRATION</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_OPTICAL_XRES</p>
<p>只读访问</p></td>
<td><p>根/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_OPTICAL_XRES</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_OPTICAL_XRES</p>
<p>只读访问</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_OPTICAL_XRES</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_OPTICAL_YRES</p>
<p>只读访问</p></td>
<td><p>根/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_OPTICAL_YRES</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_OPTICAL_YRES</p>
<p>只读访问</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_OPTICAL_YRES</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PAGES</p>
<p>读/写访问</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_PAGES</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PAGE_SIZE</p>
<p>读/写访问权限，请参阅： e</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_PAGE_SIZE</p>
<p>读/写访问权限，请参阅： e</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PAGE_WIDTH</p>
<p>只读访问</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_PAGE_WIDTH</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PAGE_HEIGHT</p>
<p>只读访问</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_PAGE_WIDTH</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PREVIEW</p>
<p>读/写访问</p></td>
<td><p>根/平板</p>
<p>请参阅备注： b</p></td>
<td><p>WIA_IPS_PREVIEW</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅备注： b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PREVIEW</p>
<p>读/写访问</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_PREVIEW</p>
<p>读/写访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_SHOW_PREVIEW_CONTROL</p>
<p>只读访问</p></td>
<td><p>根/平板</p>
<p>请参阅注意： c</p></td>
<td><p>WIA_IPS_SHOW_PREVIEW_CONTROL</p>
<p>只读访问</p></td>
<td><p>平板</p>
<p>请参阅注意： c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_SHOW_PREVIEW_CONTROL</p>
<p>只读访问</p></td>
<td><p>根/送纸器</p>
<p>请参阅备注： a</p></td>
<td><p>WIA_IPS_SHOW_PREVIEW_CONTROL</p>
<p>只读访问</p></td>
<td><p>放</p>
<p>请参阅备注： a</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>注意 a：  
 (ADF) 上的进纸器项、Windows XP 根项或子项目上的进纸器上下文 (WIA \_ DPS \_ 文档 \_ 处理 \_ 选择已设置为送) 送

<a href="" id="note-b-"></a>备注 b：  
Windows XP root 或 child 项上的平板物品或平板上下文 (WIA \_ DPS \_ 文档 \_ 处理 \_ 选择设置为平板) 

<a href="" id="note-c-"></a>备注 c：  
根项，未指定用于 Windows XP 的上下文

<a href="" id="note-d-"></a>备注 d：  
仅适用于 Windows XP 到 Windows Vista 的翻译：

\_先返回

\_仅回

模式

\_首先

\_仅限正面

\_如果未实现此属性，则默认值为 "仅限"。

备注 e：翻译所有值，而不仅仅是旧值 (WIA \_ 页面 \_ 自定义、wia \_ 页面 \_ A4、wia 页面 \_ \_ 号) 

请注意，必须将 Windows XP 根项配置为 (通过 WIA DPS 文档处理设置的相应平板/进纸器上下文集中 \_ \_ \_ \_ 选择) ，然后访问上下文相关属性， (这两种属性都可用于) 读写访问权限。

 

 




