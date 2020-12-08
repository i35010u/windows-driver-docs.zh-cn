---
title: 在不同条件下需要的显示驱动程序函数
description: 在不同条件下需要的显示驱动程序函数
keywords:
- 图形 DDI 函数 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410d1b7bb3eae81fe0f436bd015c83db4971e635
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810193"
---
# <a name="conditionally-required-display-driver-functions"></a>在不同条件下需要的显示驱动程序函数


## <span id="ddk_conditionally_required_display_driver_functions_gg"></span><span id="DDK_CONDITIONALLY_REQUIRED_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


根据驱动程序的实现方式和基础适配器的功能，可能需要其他图形 DDI 函数。 例如，如果驱动程序管理自己的 surface (使用 [**EngCreateDeviceSurface**](/windows/win32/api/winddi/nf-winddi-engcreatedevicesurface) 来获取 surface) 的句柄，则该驱动程序还必须至少支持以下 [绘制函数](optional-display-driver-functions.md)：

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvcopybits)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p>转换设备托管的光栅图面和 GDI 标准格式的位图。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstrokepath)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p>绘制 (曲线或直线) 的路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvtextout)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p>呈现指定位置的一组字形。</p></td>
</tr>
</tbody>
</table>

 

**注意**   为任何给定的图面序列化驱动程序调用。

 

写入标准格式 *dib* 的驱动程序通常允许 GDI 管理其中的大多数或全部操作。 支持可 *设置调色板* 的显示必须支持 [**DrvSetPalette**](/windows/win32/api/winddi/nf-winddi-drvsetpalette) 函数。

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvsetpalette" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvsetpalette)"><strong>DrvSetPalette</strong></a></p></td>
<td align="left"><p>请求驱动程序实现指定设备的调色板。 驱动程序将硬件调色板设置为与给定调色板中的条目尽可能匹配。</p></td>
</tr>
</tbody>
</table>

 

所有图形驱动程序的有条件必需函数的列表显示在有 [条件地需要图形驱动程序函数](conditionally-required-graphics-driver-functions.md)中。

