---
title: 指定 GDI 硬件加速的呈现操作
description: 指定 GDI 硬件加速的呈现操作
ms.assetid: 71eb9cdf-0448-48d1-835a-84bbbba13670
keywords:
- 呈现 GDI WDK 显示采用硬件加速的操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35e67aa705c8eca6d9243cccd72fc4ed8f7661a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524331"
---
# <a name="specifying-gdi-hardware-accelerated-rendering-operations"></a>指定 GDI 硬件加速的呈现操作


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


当[ **DxgkDdiRenderKm** ](https://msdn.microsoft.com/library/windows/hardware/ff559800)函数被调用时，操作系统指定 GDI 硬件加速呈现要执行的操作通过类型*pRenderKmArgs*参数。 显示端口驱动程序的 DirectX 图形内核子系统 (*Dxgkrnl.sys*) 设置*pRenderKmArgs*-&gt;**pCommand**成员添加到指向包含变量大小的数组的命令缓冲区[ **DXGK\_RENDERKM\_命令**](https://msdn.microsoft.com/library/windows/hardware/ff562026)结构。 它还设置*pRenderKmArgs*-&gt;**pCommandLength**成员添加到命令缓冲区，以字节为单位的大小。

该驱动程序必须将转换输入 DXGK\_RENDERKM\_命令命令到 DMA 缓冲区命令缓冲区，并生成该修补程序位置列表。

DXGK\_RENDERKM\_命令包含指定的 GDI 硬件加速的呈现操作的特性的成员，如下表中所述。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">呈现操作</th>
<th align="left">DXGK_RENDERKM_COMMAND 成员</th>
<th align="left">相应的 DXGK_GDIARG_XXX 结构</th>
<th align="left">相应 DXGK_RENDERKM_OPERATION 值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>alpha 混合</p></td>
<td align="left"><p>AlphaBlend</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561074" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_ALPHABLEND&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561074)"><strong>DXGK_GDIARG_ALPHABLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_ALPHABLEND = 3</p></td>
</tr>
<tr class="even">
<td align="left"><p>位块传输不拉伸的情况</p></td>
<td align="left"><p>BitBlt</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561079" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_BITBLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561079)"><strong>DXGK_GDIARG_BITBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_BITBLT = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClearType 和消除锯齿的文本像素 blend</p></td>
<td align="left"><p>ClearTypeBlend</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561082" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_CLEARTYPEBLEND&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561082)"><strong>DXGK_GDIARG_CLEARTYPEBLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_CLEARTYPEBLEND = 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>填充颜色</p></td>
<td align="left"><p>ColorFill</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561083" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_COLORFILL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561083)"><strong>DXGK_GDIARG_COLORFILL</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_COLORFILL = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>拉伸位块传输</p></td>
<td align="left"><p>StretchBlt</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561089" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_STRETCHBLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561089)"><strong>DXGK_GDIARG_STRETCHBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_STRETCHBLT = 4</p></td>
</tr>
<tr class="even">
<td align="left"><p>使用透明度位块传输</p></td>
<td align="left"><p>TransparentBlt</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561091" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_TRANSPARENTBLT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561091)"><strong>DXGK_GDIARG_TRANSPARENTBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_TRANSPARENTBLT = 6</p></td>
</tr>
</tbody>
</table>

 

操作系统使用**操作码**DXGK 成员\_RENDERKM\_命令来指示显示微型端口驱动程序必须处理的特定 GDI 硬件加速的呈现操作。 **操作码**成员是类型[ **DXGK\_RENDERKM\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff562029)，与表中显示的值。

操作系统还提供适当的值的 DXGK\_RENDERKM\_命令**CommandSize**成员，以字节为单位，包括的值指定的当前呈现命令，大小**操作码**和命令中的子矩形的数量。

中提供有关功能的显示适配器使用透明度执行位块传输的信息进一步[ **D3DKM\_TRANSPARENTBLTFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff548468)包含结构在 DXGK\_GDIARG\_TRANSPARENTBLT-&gt;**标志**成员。

 

 





