---
title: 指定 GDI 硬件加速渲染操作
description: 指定 GDI 硬件加速渲染操作
ms.assetid: 71eb9cdf-0448-48d1-835a-84bbbba13670
keywords:
- 带有 GDI 硬件加速 WDK 显示的渲染操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f92d668be6bd642b8d87d3dc21c4620c27fbcf5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825725"
---
# <a name="specifying-gdi-hardware-accelerated-rendering-operations"></a>指定 GDI 硬件加速渲染操作


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


调用[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数时，操作系统将通过*pRenderKmArgs*参数指定要执行的 GDI 硬件加速呈现操作的类型。 DirectX 图形内核子系统（*Dxgkrnl*）的显示端口驱动程序将*pRenderKmArgs*-设置&gt;**pCommand**成员，以指向包含可变大小 DXGK 数组的命令缓冲区[ **\_RENDERKM\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_renderkm_command)结构。 它还将&gt;**pCommandLength**成员的*pRenderKmArgs*-设置为命令缓冲区的大小（以字节为单位）。

驱动程序必须将输入 DXGK\_RENDERKM\_命令命令缓冲区转换为 DMA 缓冲区命令并构建修补程序位置列表。

DXGK\_RENDERKM\_命令包含一些成员，这些成员指定 GDI 硬件加速呈现操作的特性，如下表所述。

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
<th align="left">对应的 DXGK_GDIARG_XXX 结构</th>
<th align="left">对应的 DXGK_RENDERKM_OPERATION 值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>alpha blend</p></td>
<td align="left"><p>AlphaBlend</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_ALPHABLEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend)"><strong>DXGK_GDIARG_ALPHABLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_ALPHABLEND = 3</p></td>
</tr>
<tr class="even">
<td align="left"><p>无拉伸的位块传输</p></td>
<td align="left"><p>BitBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_BITBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt)"><strong>DXGK_GDIARG_BITBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_BITBLT = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ClearType 和消除锯齿文本像素 blend</p></td>
<td align="left"><p>ClearTypeBlend</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_CLEARTYPEBLEND&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend)"><strong>DXGK_GDIARG_CLEARTYPEBLEND</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_CLEARTYPEBLEND = 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>颜色填充</p></td>
<td align="left"><p>ColorFill</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_COLORFILL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill)"><strong>DXGK_GDIARG_COLORFILL</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_COLORFILL = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>延伸位块传输</p></td>
<td align="left"><p>StretchBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_STRETCHBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt)"><strong>DXGK_GDIARG_STRETCHBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_STRETCHBLT = 4</p></td>
</tr>
<tr class="even">
<td align="left"><p>具有透明度的位块传输</p></td>
<td align="left"><p>TransparentBlt</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt" data-raw-source="[&lt;strong&gt;DXGK_GDIARG_TRANSPARENTBLT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt)"><strong>DXGK_GDIARG_TRANSPARENTBLT</strong></a></p></td>
<td align="left"><p>DXGK_GDIOP_TRANSPARENTBLT = 6</p></td>
</tr>
</tbody>
</table>

 

操作系统使用 DXGK\_RENDERKM\_命令的**OpCode**成员来指明显示微型端口驱动程序必须处理的特定 GDI 硬件加速呈现操作。 **OpCode**成员的类型为[**DXGK\_RENDERKM\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_renderkm_operation)，其值显示在表中。

操作系统还将提供 DXGK\_RENDERKM\_COMMAND **CommandSize**成员的适当值，该成员指定当前呈现命令的大小（以字节为单位），包括**OpCode**的值和数字命令中的子矩形。

DXGK\_GDIARG\_TRANSPARENTBLT 中包含的[**D3DKM\_TRANSPARENTBLTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_d3dkm_transparentbltflags)结构中提供了有关显示适配器的功能，以执行具有透明度的位块传输的详细信息&gt;**标志**成员。

 

 





