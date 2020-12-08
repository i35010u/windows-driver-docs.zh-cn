---
title: WIA \_ IP \_ 打印机 \_ ENDORSER \_ 图形 \_ 位置
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ graphics \_ position 属性用于配置图像相对于要打印/认可的文本内容)  (图像的位置。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_POSITION 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_POSITION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63a939c84644de4d11ac4e29036e318b108f2327
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823127"
---
# <a name="wia_ips_printer_endorser_graphics_position"></a>WIA \_ IP \_ 打印机 \_ ENDORSER \_ 图形 \_ 位置


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ graphics \_ position** 属性用于配置图像相对于要打印/认可的文本内容)  (图像的位置。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表介绍了在 **WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 图形 \_ 位置** 中有效的常量。

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
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_LEFT</p></td>
<td><p>图像在 imprinter/endorser 区域的左侧打印/认可。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_RIGHT</p></td>
<td><p>图像在 imprinter/endorser 区域的右侧打印/认可。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP</p></td>
<td><p>图像在 imprinter/endorser 区域的顶部打印/认可。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM</p></td>
<td><p>图像在 imprinter/endorser 区域的底部打印/认可。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP_LEFT</p></td>
<td><p>图像在 imprinter/endorser 区域的左上角进行打印/认可。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP_RIGHT</p></td>
<td><p>图像在 imprinter/endorser 区域的右上角进行打印/认可。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM_LEFT</p></td>
<td><p>图像在 imprinter/endorser 区域的左下角进行打印/认可。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM_RIGHT</p></td>
<td><p>图像在 imprinter/endorser 区域的右下角进行打印/认可。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BACKGROUND</p></td>
<td><p>图像将打印/认可为背景，并通过图像打印/认可文本。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_RANDOM</p></td>
<td><p>图像在设备选择的随机位置上打印/认可。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_ GRAPHICS_DEVICE_DEFAULT</p></td>
<td><p>此图像将按设备选择的默认 (首选) 位置打印/认可。</p></td>
</tr>
</tbody>
</table>

 

\_ \_ \_ \_ 当支持此属性时，WIA PRINTER ENDORSER GRAPHICS DEVICE \_ 默认值是所有 Imprinter/ENDORSER 项都必须支持的默认值。

此属性是必需的，对于为 [**WIA \_ IPS \_ PRINTER \_ Endorser \_ 图形**](wia-ips-printer-endorser-graphics.md)报告非零 (True) 值的所有 Imprinter/Endorser 项都有效。 否则，属性无效。

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

 

 





