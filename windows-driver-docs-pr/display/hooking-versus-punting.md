---
title: 挂钩与转移
description: 挂钩与转移
ms.assetid: 52544915-8392-4eb1-8186-6a7fbad8ed4a
keywords:
- 图面上协商 WDK GDI，挂钩
- 图面协商 WDK GDI，punting
- 挂接 WDK GDI
- punting WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdec2fc10f763a97677a46b65f684a7ded760a85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380221"
---
# <a name="hooking-versus-punting"></a>挂钩与转移


## <span id="ddk_hooking_versus_punting_gg"></span><span id="DDK_HOOKING_VERSUS_PUNTING_GG"></span>


条款*挂接*并*punting*指代是否提供了标准位图绘制操作，或依赖于 GDI 上的驱动程序决策，让他们。 如果该驱动程序实现引擎管理面，GDI 可以处理所有绘制操作。 驱动程序可以但是，提供一种或多种[的绘图功能](optional-display-driver-functions.md)如果其硬件可以加速这些操作。 这是通过实现，或挂钩*DrvXxx*函数。

驱动程序编写者可能想要实现特定图形 DDI 入口点实现的绘制操作的一个子集。 对于该驱动程序不支持任何操作，它可以调用适当的 GDI 函数，来执行操作。这称为 punting 到 GDI。 有某些情况下，在驱动程序必须在其中实现该操作。 例如，如果驱动程序实现设备管理面，必须显示驱动程序中实现某些绘图函数。

### <a name="span-idhookingspanspan-idhookingspanspan-idhookingspanhooking"></a><span id="Hooking"></span><span id="hooking"></span><span id="HOOKING"></span>挂接

默认情况下，绘图图面时是引擎托管的表面，GDI 绘图 （呈现） 对操作进行处理。 若要充分利用提供的某些或全部给定表面，这些绘图函数加速的硬件或使驱动程序的使用特殊的块传输硬件，它可以将这些函数挂钩。 要将连接的调用，该驱动程序指定挂钩作为标志的*flHook*的参数[ **EngAssociateSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engassociatesurface)并[ **EngModifySurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmodifysurface)函数。

如果该驱动程序指定一个函数的挂钩标志，它必须提供该函数在其列表中的受支持的图形 DDI 入口点。 该驱动程序可以优化操作没有硬件支持。 此类驱动程序可能会处理仅在已挂钩调用某些情况。 例如，如果复杂的图形请求上挂接的调用，可能仍会被迫回调到 GDI，从而允许 GDI 来处理操作效率更高。

下面是可以选择是否要处理已挂钩的呼叫的驱动程序的另一个示例。 支持可用于处理位块传送调用某特定的硬件的驱动程序，请考虑*ROPs*。 即使此驱动程序可以执行自己的许多操作，否则是只需帧缓冲区。 这样的驱动程序将一个句柄与帧缓冲区位图图面返回的图面作为其*PDEV*，但它将挂钩[ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)为自身调用。 当调用 GDI *DrvBitBlt*，驱动程序可以检查 ROP 以查看它是否由硬件支持的其中一个。 如果不是，该驱动程序可以将操作传递回调用 GDI [ **EngBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt)函数。

支持设备管理 surface 驱动程序必须挂接查看一些绘图函数;namely [ **DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)， [ **DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)，并[ **DrvStrokePath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath). 尽管 GDI 模拟可以处理其他绘图函数，但建议出于性能原因，此类型挂接的驱动程序如出其他函数[ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)和[**DrvRealizeBrush** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)函数，因为模拟需要绘制从 / 向在图面。

### <a name="span-idpuntingspanspan-idpuntingspanspan-idpuntingspanpunting"></a><span id="Punting"></span><span id="punting"></span><span id="PUNTING"></span>Punting

*Punting*到 GDI 回调意味着将放入相应的 GDI 模拟调用中。 一般情况下，为每个*DrvXxx*图形调用没有对应的 GDI **Eng * * * Xxx*模拟调用使用相同的参数。 只要该驱动程序进行了位图 nonopaque，可以将所有参数而无需更改都传递到 GDI 模拟。 对于每个调用回 GDI punts 驱动程序，驱动程序的大小被减少 （因为该功能的代码，则可以省略）。 但是，因为该引擎负责调用，该驱动程序不具有控制的执行速度。 对于某些复杂的情况下，可能没有真正的优势提供的驱动程序支持。

### <a name="span-idhookablegdigraphicsoutputfunctionsspanspan-idhookablegdigraphicsoutputfunctionsspanspan-idhookablegdigraphicsoutputfunctionsspanhookable-gdi-graphics-output-functions"></a><span id="Hookable_GDI_Graphics_Output_Functions"></span><span id="hookable_gdi_graphics_output_functions"></span><span id="HOOKABLE_GDI_GRAPHICS_OUTPUT_FUNCTIONS"></span>可钩进 GDI 图形输出函数

图形输出函数，该驱动程序可以挂接和下表中列出了相应的 GDI 模拟。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序的图形输出函数</th>
<th align="left">相应的 GDI 模拟</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)"><strong>DrvBitBlt</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt" data-raw-source="[&lt;strong&gt;EngBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engbitblt)"><strong>EngBitBlt</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)"><strong>DrvPlgBlt</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt" data-raw-source="[&lt;strong&gt;EngPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engplgblt)"><strong>EngPlgBlt</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"><strong>DrvStretchBlt</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt" data-raw-source="[&lt;strong&gt;EngStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchblt)"><strong>EngStretchBlt</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)"><strong>DrvStretchBltROP</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop" data-raw-source="[&lt;strong&gt;EngStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstretchbltrop)"><strong>EngStretchBltROP</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtextout" data-raw-source="[&lt;strong&gt;EngTextOut&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtextout)"><strong>EngTextOut</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath" data-raw-source="[&lt;strong&gt;EngStrokePath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath)"><strong>EngStrokePath</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)"><strong>DrvFillPath</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath" data-raw-source="[&lt;strong&gt;EngFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath)"><strong>EngFillPath</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)"><strong>DrvStrokeAndFillPath</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath" data-raw-source="[&lt;strong&gt;EngStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokeandfillpath)"><strong>EngStrokeAndFillPath</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)"><strong>DrvLineTo</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto" data-raw-source="[&lt;strong&gt;EngLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englineto)"><strong>EngLineTo</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits" data-raw-source="[&lt;strong&gt;EngCopyBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcopybits)"><strong>EngCopyBits</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)"><strong>DrvAlphaBlend</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend" data-raw-source="[&lt;strong&gt;EngAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engalphablend)"><strong>EngAlphaBlend</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"><strong>DrvGradientFill</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill" data-raw-source="[&lt;strong&gt;EngGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggradientfill)"><strong>EngGradientFill</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"><strong>DrvTransparentBlt</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt" data-raw-source="[&lt;strong&gt;EngTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engtransparentblt)"><strong>EngTransparentBlt</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





