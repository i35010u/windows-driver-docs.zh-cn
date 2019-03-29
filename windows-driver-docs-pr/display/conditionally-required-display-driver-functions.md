---
title: 在不同条件下需要的显示驱动程序函数
description: 在不同条件下需要的显示驱动程序函数
ms.assetid: c2de7e48-2ce6-466f-947e-bdac1d4fe422
keywords:
- 显示图形 DDI 函数 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 941ba5b6c0714059ef8c94f32bfafb2d5b23779e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576230"
---
# <a name="conditionally-required-display-driver-functions"></a>在不同条件下需要的显示驱动程序函数


## <span id="ddk_conditionally_required_display_driver_functions_gg"></span><span id="DDK_CONDITIONALLY_REQUIRED_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


具体取决于如何实现一个驱动程序和功能的基础适配器，可能需要其他图形 DDI 函数。 例如，如果驱动程序管理其自己图面 (使用[ **EngCreateDeviceSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564206)若要获取的句柄在图面)，该驱动程序还必须至少支持以下[绘图函数](optional-display-driver-functions.md):

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556182" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556182)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p>设备管理光栅图面和 GDI 标准格式位图之间进行转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556316" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556316)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p>当绘制 （曲线或行） 的路径由 GDI 调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557277" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557277)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p>呈现一组指定位置处的标志符号。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  驱动程序调用进行序列化的任何给定的图面。

 

为标准格式编写的驱动程序*Dib*通常允许 GDI 来管理大多数或所有这些操作。 显示该功能的支持*可设置调色板*必须支持[ **DrvSetPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff556282)函数。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556282" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556282)"><strong>DrvSetPalette</strong></a></p></td>
<td align="left"><p>请求驱动程序意识到指定设备的调色板。 该驱动程序设置硬件调色板以尽可能接近地匹配给定调色板中的条目。</p></td>
</tr>
</tbody>
</table>

 

有条件地所需的所有图形驱动程序的功能列表将显示在[有条件地所需的图形驱动程序函数](conditionally-required-graphics-driver-functions.md)。

 

 





