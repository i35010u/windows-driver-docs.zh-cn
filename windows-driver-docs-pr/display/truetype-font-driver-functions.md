---
title: TrueType 字体驱动程序函数
description: TrueType 字体驱动程序函数
ms.assetid: 9ed59393-c4a6-4d3f-9a18-c9e5493c2dc9
keywords:
- 字体 WDK 图形，TrueType 驱动程序函数
- GDI WDK Windows 2000 显示、 字体、 TrueType 驱动程序函数
- 图形驱动程序 WDK Windows 2000 显示，字体，TrueType 驱动程序功能
- TrueType 字体驱动程序 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b85efd35685036a3a523bfcc4e331e739589103
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547650"
---
# <a name="truetype-font-driver-functions"></a>TrueType 字体驱动程序函数


## <span id="ddk_truetype_font_driver_functions_gg"></span><span id="DDK_TRUETYPE_FONT_DRIVER_FUNCTIONS_GG"></span>


TrueType 字体驱动程序必须支持下表中列出的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556235" data-raw-source="[&lt;strong&gt;DrvGetTrueTypeFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556235)"><strong>DrvGetTrueTypeFile</strong></a></p></td>
<td align="left"><p>内存映射 TrueType 字体文件，GDI 高效访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556269" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeOutline&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556269)"><strong>DrvQueryTrueTypeOutline</strong></a></p></td>
<td align="left"><p>Native TrueType 格式返回标志符号句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556271" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556271)"><strong>DrvQueryTrueTypeTable</strong></a></p></td>
<td align="left"><p>TrueType 字体文件格式中的特定文件，GDI 访问。</p></td>
</tr>
</tbody>
</table>

 

所有这些函数将 GDI 提供有关 TrueType 字体文件的信息。 *DrvQueryTrueTypeTable*应授予对特定表中的 TrueType 字体文件格式的 GDI 访问权限。 *DrvQueryTrueTypeOutline*必须以本机 TrueType 格式发送 GDI 字形轮廓。 *DrvGetTrueTypeFile*返回到 GDI TrueType 驱动程序的专用入口点，GDI 高效地访问内存映射 TrueType 字体文件。

 

 





