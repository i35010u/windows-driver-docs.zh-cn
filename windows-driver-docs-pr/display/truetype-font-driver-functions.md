---
title: TrueType 字体驱动程序函数
description: TrueType 字体驱动程序函数
ms.assetid: 9ed59393-c4a6-4d3f-9a18-c9e5493c2dc9
keywords:
- 字体 WDK 图形，TrueType 驱动程序函数
- GDI WDK Windows 2000 显示、字体、TrueType 驱动程序函数
- 图形驱动程序 WDK Windows 2000 显示、字体、TrueType 驱动程序函数
- TrueType 字体驱动程序 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e3c5c4f5832022e5cd9f9a409e8cb59a005eeda
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067172"
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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgettruetypefile" data-raw-source="[&lt;strong&gt;DrvGetTrueTypeFile&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvgettruetypefile)"><strong>DrvGetTrueTypeFile</strong></a></p></td>
<td align="left"><p>赋予 GDI 对内存映射的 TrueType 字体文件的有效访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerytruetypeoutline" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeOutline&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvquerytruetypeoutline)"><strong>DrvQueryTrueTypeOutline</strong></a></p></td>
<td align="left"><p>返回本机 TrueType 格式的标志符号句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerytruetypetable" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeTable&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvquerytruetypetable)"><strong>DrvQueryTrueTypeTable</strong></a></p></td>
<td align="left"><p>为 TrueType 字体文件格式的特定文件提供 GDI 访问。</p></td>
</tr>
</tbody>
</table>

 

所有这些函数都为 GDI 提供有关 TrueType 字体文件的信息。 *DrvQueryTrueTypeTable* 应为 TrueType 字体文件格式的特定表授予 GDI 访问权限。 *DrvQueryTrueTypeOutline* 必须发送本机 TrueType 格式的 GDI 标志符号大纲。 *DrvGetTrueTypeFile* 会将 TrueType 驱动程序的私有入口点返回到 gdi，这允许 gdi 有效访问内存映射的 TrueType 字体文件。

 

