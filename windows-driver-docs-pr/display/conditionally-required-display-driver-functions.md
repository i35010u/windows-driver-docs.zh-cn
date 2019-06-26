---
title: 在不同条件下需要的显示驱动程序函数
description: 在不同条件下需要的显示驱动程序函数
ms.assetid: c2de7e48-2ce6-466f-947e-bdac1d4fe422
keywords:
- 显示图形 DDI 函数 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51abdf0ab2d169d97a8f32022b47a5dcd4867220
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375397"
---
# <a name="conditionally-required-display-driver-functions"></a>在不同条件下需要的显示驱动程序函数


## <span id="ddk_conditionally_required_display_driver_functions_gg"></span><span id="DDK_CONDITIONALLY_REQUIRED_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


具体取决于如何实现一个驱动程序和功能的基础适配器，可能需要其他图形 DDI 函数。 例如，如果驱动程序管理其自己图面 (使用[ **EngCreateDeviceSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface)若要获取的句柄在图面)，该驱动程序还必须至少支持以下[绘图函数](optional-display-driver-functions.md):

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p>设备管理光栅图面和 GDI 标准格式位图之间进行转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p>当绘制 （曲线或行） 的路径由 GDI 调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p>呈现一组指定位置处的标志符号。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  驱动程序调用进行序列化的任何给定的图面。

 

为标准格式编写的驱动程序*Dib*通常允许 GDI 来管理大多数或所有这些操作。 显示该功能的支持*可设置调色板*必须支持[ **DrvSetPalette** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)函数。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)"><strong>DrvSetPalette</strong></a></p></td>
<td align="left"><p>请求驱动程序意识到指定设备的调色板。 该驱动程序设置硬件调色板以尽可能接近地匹配给定调色板中的条目。</p></td>
</tr>
</tbody>
</table>

 

有条件地所需的所有图形驱动程序的功能列表将显示在[有条件地所需的图形驱动程序函数](conditionally-required-graphics-driver-functions.md)。

 

 





