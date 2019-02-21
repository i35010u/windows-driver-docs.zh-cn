---
title: WIA\_IPS\_文档\_处理\_选择
description: WIA\_IPS\_文档\_处理\_选择属性包含的当前扫描程序获取源和模式。
ms.assetid: f148e91f-847c-4db2-8459-9f52892cd703
keywords:
- WIA_IPS_DOCUMENT_HANDLING_SELECT 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_DOCUMENT_HANDLING_SELECT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 387850c5e7a7baab4af22e4e4dd2ddcfdec59fa4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523952"
---
# <a name="wiaipsdocumenthandlingselect"></a>WIA\_IPS\_文档\_处理\_选择


WIA\_IPS\_文档\_处理\_选择属性包含的当前扫描程序获取源和模式。

属性类型：VT\_I4

有效值：WIA\_PROP\_FLAG

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPS\_文档\_处理\_选择属性，以确定当前获取源的扫描程序或应用程序将此属性设置的源和模式的写入扫描程序。 此外，应用程序使用此属性来启用和禁用双面打印器功能。 WIA 微型驱动程序创建并维护此属性。

下表描述了一个常量，它是有效使用 Windows Vista 及更高版本。

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
<td><p>ADVANCED_DUPLEX</p></td>
<td><p>通过使用单独的配置设置为每个送纸器子项 （WIA_CATEGORY_FEEDER_FRONT 和 WIA_CATEGORY_FEEDER_BACK） 扫描。 不能与双工设置此标志。</p>
<p>设备支持不同扫描前面的设置和备份的项应实现可选的 ADF 前端和后的项，以及它应支持双工和 ADVANCED_DUPLEX。</p></td>
</tr>
</tbody>
</table>

 

下表描述了与 Windows Vista 和 Windows XP 有效的常量。

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
<td><p>BACK_FIRST</p></td>
<td><p>第一次扫描的文档。 仅当双工设置时，此值才有效。</p></td>
</tr>
<tr class="even">
<td><p>BACK_ONLY</p></td>
<td><p>扫描背面<em>仅</em>。 仅当双工设置时，此值才有效。</p></td>
</tr>
<tr class="odd">
<td><p>双工</p></td>
<td><p>使用双面打印器操作来扫描。</p></td>
</tr>
<tr class="even">
<td><p>FRONT_FIRST</p></td>
<td><p>第一次扫描的文档的前面。 仅当双工设置时，此值才有效。</p></td>
</tr>
<tr class="odd">
<td><p>FRONT_ONLY</p></td>
<td><p>扫描前面<em>仅</em>。</p></td>
</tr>
</tbody>
</table>

 

双工和前面的值\_仅是互相排斥-设置一个或另一个，但不可同时使用两者。

WIA 2.0 微型驱动程序必须将此属性的初始值设置为其默认值，前端\_仅。 不遵守此要求可能会使微型驱动程序与 WIA 1.0 通用扫描对话框以及一些 WIA 1.0 应用程序不兼容。

下表描述了与 Windows XP 有效，但已过时，与 Windows Vista 及更高版本的常量。

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
<td><p>AUTO_ADVANCE</p></td>
<td><p>启用扫描后的下一个文档的自动维护。</p></td>
</tr>
<tr class="even">
<td><p>送纸器</p></td>
<td><p>通过使用文档送纸器扫描。</p></td>
</tr>
<tr class="odd">
<td><p>平板</p></td>
<td><p>通过使用平板扫描。</p></td>
</tr>
<tr class="even">
<td><p>NEXT_PAGE</p></td>
<td><p>扫描文档的下一页面。</p></td>
</tr>
<tr class="odd">
<td><p>PREFEED</p></td>
<td><p>启用预源的模式。 扫描时的下一个文档的位置。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中可用。 对于 Windows XP 中，使用相同的 WIA_DPS_DOCUMENT_HANDLING_SELECT 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_DPS\_文档\_处理\_选择**](wia-dps-document-handling-select.md)

 

 






