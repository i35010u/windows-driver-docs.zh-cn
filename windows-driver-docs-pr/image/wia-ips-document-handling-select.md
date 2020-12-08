---
title: WIA \_ IP \_ 文档 \_ 处理 \_ 选择
description: WIA \_ ip \_ 文档 \_ 处理 \_ 选择属性包含当前的扫描仪获取源和模式。
keywords:
- WIA_IPS_DOCUMENT_HANDLING_SELECT 图像设备
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
ms.openlocfilehash: 8635328314de8df427d724e97be4134c332b0a63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796129"
---
# <a name="wia_ips_document_handling_select"></a>WIA \_ IP \_ 文档 \_ 处理 \_ 选择


WIA \_ ip \_ 文档 \_ 处理 \_ 选择属性包含当前的扫描仪获取源和模式。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 标志

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ ip \_ 文档 \_ 处理 \_ 选择属性以确定扫描仪的当前采集源，或者应用程序写入此属性以设置扫描程序的源和模式。 此外，应用程序使用此属性来启用和禁用双面打印器功能。 WIA 微型驱动程序创建并维护此属性。

下表描述了仅适用于 Windows Vista 和更高版本的常量。

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
<td><p>使用各个子送纸器项的单独配置设置进行扫描 (WIA_CATEGORY_FEEDER_FRONT 和 WIA_CATEGORY_FEEDER_BACK) 。 此标志不能与双工一起设置。</p>
<p>支持对前面和背面项的不同扫描设置的设备应实现可选的 ADF 前端和后端，并且它应同时支持双工和 ADVANCED_DUPLEX。</p></td>
</tr>
</tbody>
</table>

 

下表介绍了 Windows Vista 和 Windows XP 中的有效常量。

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

WIA 2.0 微型驱动程序必须将此属性的初始值设置为其默认值 " \_ 仅限前"。 如果无法遵守这种要求，则可能导致微型驱动程序与 WIA 1.0 常见扫描对话框和某些 WIA 1.0 应用程序不兼容。

下表描述了对 Windows XP 有效但在 Windows Vista 和更高版本中已过时的常量。

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
<td><p>启用预供给模式。 在扫描时定位下一文档。</p></td>
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
<td><p>在 Windows Vista 和更高版本的操作系统中可用。 对于 Windows XP，请使用相同的 WIA_DPS_DOCUMENT_HANDLING_SELECT 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ 文档 \_ 处理 \_ 选择**](wia-dps-document-handling-select.md)

 

 






