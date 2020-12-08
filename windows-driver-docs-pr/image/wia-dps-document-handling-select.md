---
title: WIA \_ DPS \_ 文档 \_ 处理 \_ 选择
description: WIA \_ DPS \_ 文档 \_ 处理 \_ 选择属性包含当前的扫描仪获取源和模式。
keywords:
- WIA_DPS_DOCUMENT_HANDLING_SELECT 图像设备
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
ms.openlocfilehash: 3e72d69f1afdb25524f1c49bad45ee13c9ae25ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836997"
---
# <a name="wia_dps_document_handling_select"></a>WIA \_ DPS \_ 文档 \_ 处理 \_ 选择


WIA \_ DPS \_ 文档 \_ 处理 \_ 选择属性包含当前的扫描仪获取源和模式。

## <span id="ddk_wia_dps_document_handling_select_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_SELECT_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 标志

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ DPS \_ 文档 \_ 处理 \_ 选择属性以确定扫描仪的当前采集源，或使用应用程序编写此属性来设置扫描程序的源和模式。 此外，应用程序使用此属性来启用和禁用双面打印器功能。 WIA 微型驱动程序创建并维护此属性。

下表描述了对 WIA \_ DPS \_ 文档 \_ 处理选择有效的常量 \_ 。

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
<td><p>首先扫描文档的背面。 仅当设置了双工时，此值才有效。</p></td>
</tr>
<tr class="even">
<td><p>BACK_ONLY</p></td>
<td><p><em>仅</em>扫描后退。 仅当设置了双工时，此值才有效。</p></td>
</tr>
<tr class="odd">
<td><p>模式</p></td>
<td><p>使用双面打印器操作进行扫描。</p></td>
</tr>
<tr class="even">
<td><p>FRONT_FIRST</p></td>
<td><p>首先扫描文档的前面。 仅当设置了双工时，此值才有效。</p></td>
</tr>
<tr class="odd">
<td><p>FRONT_ONLY</p></td>
<td><p><em>仅</em>扫描前端。</p></td>
</tr>
</tbody>
</table>

 

值双工和前端 \_ 仅互斥--设置一个或另一个，但不能同时为两者。

下表描述了与 Microsoft Windows XP 一起具有此属性的常量，但在 Windows Vista 和更高版本中已过时。

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
<td><p>扫描后，启用下一文档的自动馈送。</p></td>
</tr>
<tr class="even">
<td><p>放</p></td>
<td><p>使用文档送纸器进行扫描。</p></td>
</tr>
<tr class="odd">
<td><p>平板</p></td>
<td><p>使用平板扫描。</p></td>
</tr>
<tr class="even">
<td><p>NEXT_PAGE</p></td>
<td><p>扫描文档的下一页。</p></td>
</tr>
<tr class="odd">
<td><p>PREFEED</p></td>
<td><p>启用预供给模式。 扫描时介词下一文档。</p></td>
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
<td><p>适用于 Microsoft Windows XP。 对于 Windows Vista 和更高版本，请使用 WIA_IPS_DOCUMENT_HANDLING_SELECT 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IP \_ 文档 \_ 处理 \_ 选择**](wia-ips-document-handling-select.md)

 

 






