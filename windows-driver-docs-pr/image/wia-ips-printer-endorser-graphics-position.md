---
title: WIA\_IPS\_打印机\_印记签署器\_图形\_位置
description: WIA\_IPS\_打印机\_印记签署器\_图形\_POSITION 属性用于配置映像 （图形） 的位置相对于要打印/认可的文本内容。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: CB7B84F0-A585-49AB-ADDE-039C2D415E72
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_POSITION 成像设备
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
ms.openlocfilehash: 657f8ed9931624b1a7ef80d08dd555d844c735ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566098"
---
# <a name="wiaipsprinterendorsergraphicsposition"></a>WIA\_IPS\_打印机\_印记签署器\_图形\_位置


**WIA\_IPS\_打印机\_印记签署器\_图形\_位置**属性用于配置的位置相对于文本内容的映像 （图形）要打印/认可。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了与有效的常量**WIA\_IPS\_打印机\_印记签署器\_图形\_位置**。

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
<td><p>映像是在左侧和右侧的打印/认可的印刷器/印记签署器区域。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_RIGHT</p></td>
<td><p>映像是在右侧的打印/认可的印刷器/印记签署器区域。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP</p></td>
<td><p>映像是在顶部打印/认可的印刷器/印记签署器区域。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM</p></td>
<td><p>映像是在底部打印/认可的印刷器/印记签署器区域。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP_LEFT</p></td>
<td><p>该映像已打印/认可的左上角的印刷器/印记签署器区域。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_TOP_RIGHT</p></td>
<td><p>该映像已打印/认可的右上角的印刷器/印记签署器区域。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM_LEFT</p></td>
<td><p>该映像已打印/认可的左下角的印刷器/印记签署器区域。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BOTTOM_RIGHT</p></td>
<td><p>该映像已打印/认可的右下角的印刷器/印记签署器区域。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_BACKGROUND</p></td>
<td><p>打印/认可的作为背景图像，并且文本打印/认可图像上方。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_GRAPHICS_RANDOM</p></td>
<td><p>该映像选择的设备的随机位置已打印/认可。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_ GRAPHICS_DEVICE_DEFAULT</p></td>
<td><p>映像选择的设备 （首选） 的默认位置是打印/认可。</p></td>
</tr>
</tbody>
</table>

 

WIA\_打印机\_印记签署器\_图形\_设备\_默认值是印刷器/印记签署器的所有项必须都支持此属性支持时所需的默认值。

此属性是必需的和有效的所有印刷器/印记签署器项的报告值为非零值 (True)，以便[ **WIA\_IPS\_打印机\_印记签署器\_图形**](wia-ips-printer-endorser-graphics.md). 否则，该属性是无效。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





