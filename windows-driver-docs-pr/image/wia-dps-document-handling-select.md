---
title: WIA\_DPS\_文档\_处理\_选择
description: WIA\_DPS\_文档\_处理\_选择属性包含的当前扫描程序获取源和模式。
ms.assetid: 17964dc5-8008-4f9c-abcd-cc72c1d6c398
keywords:
- WIA_DPS_DOCUMENT_HANDLING_SELECT 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_DOCUMENT_HANDLING_SELECT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b75d37f14a8a533f0b95ac85b809839faf7bb9fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564281"
---
# <a name="wiadpsdocumenthandlingselect"></a>WIA\_DPS\_文档\_处理\_选择


WIA\_DPS\_文档\_处理\_选择属性包含的当前扫描程序获取源和模式。

## <span id="ddk_wia_dps_document_handling_select_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_SELECT_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_FLAG

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPS\_文档\_处理\_选择属性以确定当前获取源的扫描程序或应用程序写入此属性设置的源和模式扫描程序。 此外，应用程序使用此属性来启用和禁用双面打印器功能。 WIA 微型驱动程序创建并维护此属性。

下表描述了有效使用 WIA 的常量\_DPS\_文档\_处理\_选择。

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

下表描述了与此属性与 Microsoft Windows XP 有效，但已过时，与 Windows Vista 及更高版本的常量。

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
<td><p>启用预源的模式。 扫描时介词的下一个文档。</p></td>
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
<td><p>适用于 Microsoft Windows XP。 适用于 Windows Vista 和更高版本，使用 WIA_IPS_DOCUMENT_HANDLING_SELECT 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPS\_文档\_处理\_选择**](wia-ips-document-handling-select.md)

 

 






