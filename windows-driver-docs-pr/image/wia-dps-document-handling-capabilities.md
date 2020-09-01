---
title: WIA \_ DPS \_ 文档 \_ 处理 \_ 功能
description: WIA \_ DPS \_ 文档 \_ 处理 \_ 功能属性包含扫描程序的功能。
ms.assetid: 19c9cbd0-19ef-4d44-85f1-25e71f9a92bc
keywords:
- WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 131ffde95d45089178a5377192c4cdeadbe45dd9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185285"
---
# <a name="wia_dps_document_handling_capabilities"></a>WIA \_ DPS \_ 文档 \_ 处理 \_ 功能


WIA \_ DPS \_ 文档 \_ 处理 \_ 功能属性包含扫描程序的功能。

## <span id="ddk_wia_dps_document_handling_capabilities_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序将读取 "WIA \_ DPS \_ 文档 \_ 处理功能" \_ 属性，以确定扫描仪是否安装了平板、文档送纸器或双面打印器。 你还可以使用此属性来进一步定义已安装的功能。 WIA 微型驱动程序创建并维护此属性。

下表描述了仅适用于 Windows 8 的常量。

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
<td><p>IMPRINTER</p></td>
<td><p>Imprinter</p></td>
</tr>
<tr class="even">
<td><p>ENDORSER</p></td>
<td><p>Endorser</p></td>
</tr>
<tr class="odd">
<td><p>BARCODE_READER</p></td>
<td><p>条形码读取器</p></td>
</tr>
<tr class="even">
<td><p>PATCH_CODE_READER</p></td>
<td><p>修补程序代码读取器</p></td>
</tr>
<tr class="odd">
<td><p>MICR_READER</p></td>
<td><p>磁墨</p></td>
</tr>
</tbody>
</table>

 

下表描述了仅适用于 Windows 7 的常量。

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
<td><p>AUTO_SOURCE</p></td>
<td><p>设备支持 <a href="https://docs.microsoft.com/windows-hardware/drivers/image/auto-configured-scanning" data-raw-source="[auto-configured scanning](./auto-configured-scanning.md)">自动配置的扫描</a>。</p></td>
</tr>
</tbody>
</table>

 

下表描述了对 Windows 7 和 Windows Vista 有效但在 Windows XP 中无效的常量。

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
<td><p>ADVANCED_DUP</p></td>
<td><p>设备支持高级双工扫描配置，独立于每个文档大小。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_FILM_TPA</p></td>
<td><p>扫描程序可以检测透明度或胶片扫描适配器何时准备扫描。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_STOR</p></td>
<td><p>当内部存储中存在文档时，扫描程序可以检测到该文件。</p></td>
</tr>
<tr class="even">
<td><p>FILM_TPA</p></td>
<td><p>扫描仪具有透明度或胶片扫描适配器。</p></td>
</tr>
<tr class="odd">
<td><p>STOR</p></td>
<td><p>扫描仪配有内部存储设备。</p></td>
</tr>
</tbody>
</table>

 

下表介绍了 Windows 7、Windows Vista 和 Windows XP 中的有效常量。

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
<td><p>DETECT_FEED</p></td>
<td><p>扫描仪可以检测进纸器中的文档。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_FLAT</p></td>
<td><p>扫描仪可以检测平板影印上的文档。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_SCAN</p></td>
<td><p>扫描程序只能通过扫描检测进纸器中的文档。</p></td>
</tr>
<tr class="even">
<td><p>重复</p></td>
<td><p>扫描仪有双面打印器。</p></td>
</tr>
<tr class="odd">
<td><p>馈电</p></td>
<td><p>扫描仪安装了文档送纸器。</p></td>
</tr>
<tr class="even">
<td><p>降</p></td>
<td><p>扫描仪具有平板影印。</p></td>
</tr>
</tbody>
</table>

 

下表描述了仅适用于 Windows XP 的常量;对于 Windows 7 和 Windows Vista，这些标志已过时，不应使用。

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
<td><p>DETECT_DUP</p></td>
<td><p>扫描程序可以检测来自用户的双工扫描请求。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_DUP_AVAIL</p></td>
<td><p>扫描程序可以检测到安装了双面打印器。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_FEED_AVAIL</p></td>
<td><p>扫描程序可以检测到安装文档送纸器的时间。</p></td>
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
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

