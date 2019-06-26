---
title: 指定 GDI 硬件加速渲染操作
description: 指定 GDI 硬件加速渲染操作
ms.assetid: 71eb9cdf-0448-48d1-835a-84bbbba13670
keywords:
- 呈现 GDI WDK 显示采用硬件加速的操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f10600a7813112b2a9e63c23fcd23942e86acec8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356350"
---
# <a name="specifying-gdi-hardware-accelerated-rendering-operations"></a>指定 GDI 硬件加速渲染操作


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


当[ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数被调用时，操作系统指定 GDI 硬件加速呈现要执行的操作通过类型*pRenderKmArgs*参数。 显示端口驱动程序的 DirectX 图形内核子系统 (*Dxgkrnl.sys*) 设置*pRenderKmArgs*-&gt;**pCommand**成员添加到指向包含变量大小的数组的命令缓冲区[ **DXGK\_RENDERKM\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_renderkm_command)结构。 它还设置*pRenderKmArgs*-&gt;**pCommandLength**成员添加到命令缓冲区，以字节为单位的大小。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_ALPHABLEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend)"><strong>DXGK_GDIARG_ALPHABLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_ALPHABLEND = 3</p></td>
</tr>
<tr class="even">
<td align="left"><p>位块传输不拉伸的情况</p></td>
<td align="left"><p>BitBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_BITBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt)"><strong>DXGK_GDIARG_BITBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_BITBLT = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClearType 和消除锯齿的文本像素 blend</p></td>
<td align="left"><p>ClearTypeBlend</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_CLEARTYPEBLEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend)"><strong>DXGK_GDIARG_CLEARTYPEBLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_CLEARTYPEBLEND = 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>填充颜色</p></td>
<td align="left"><p>ColorFill</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_COLORFILL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill)"><strong>DXGK_GDIARG_COLORFILL</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_COLORFILL = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>拉伸位块传输</p></td>
<td align="left"><p>StretchBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_STRETCHBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt)"><strong>DXGK_GDIARG_STRETCHBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_STRETCHBLT = 4</p></td>
</tr>
<tr class="even">
<td align="left"><p>使用透明度位块传输</p></td>
<td align="left"><p>TransparentBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_TRANSPARENTBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt)"><strong>DXGK_GDIARG_TRANSPARENTBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_TRANSPARENTBLT = 6</p></td>
</tr>
</tbody>
</table>

 

操作系统使用**操作码**DXGK 成员\_RENDERKM\_命令来指示显示微型端口驱动程序必须处理的特定 GDI 硬件加速的呈现操作。 **操作码**成员是类型[ **DXGK\_RENDERKM\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_renderkm_operation)，与表中显示的值。

操作系统还提供适当的值的 DXGK\_RENDERKM\_命令**CommandSize**成员，以字节为单位，包括的值指定的当前呈现命令，大小**操作码**和命令中的子矩形的数量。

中提供有关功能的显示适配器使用透明度执行位块传输的信息进一步[ **D3DKM\_TRANSPARENTBLTFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_d3dkm_transparentbltflags)包含结构在 DXGK\_GDIARG\_TRANSPARENTBLT-&gt;**标志**成员。

 

 





