---
title: 挂钩与转移
description: 挂钩与转移
ms.assetid: 52544915-8392-4eb1-8186-6a7fbad8ed4a
keywords:
- surface 协商 WDK GDI，挂钩
- surface 协商 WDK GDI，punting
- 挂钩 WDK GDI
- punting WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b880d82e4917311a26d843c87625b520c3c9dbd9
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716918"
---
# <a name="hooking-versus-punting"></a>挂钩与转移


## <span id="ddk_hooking_versus_punting_gg"></span><span id="DDK_HOOKING_VERSUS_PUNTING_GG"></span>


术语 " *挂钩* " 和 " *punting* " 是指驱动程序决定是否提供标准位图绘图操作，或依赖于 GDI 来提供这些操作。 如果驱动程序实现引擎管理的图面，则 GDI 可以处理所有绘图操作。 但是，如果驱动程序的硬件可以加速这些操作，则可以提供一个或多个 [绘图函数](optional-display-driver-functions.md) 。 它通过实现或挂钩 *DrvXxx* 函数来实现此功能。

驱动程序编写器可能想要仅实现特定图形 DDI 入口点所实现的一部分绘图操作。 对于该驱动程序不支持的任何操作，它可以调用适当的 GDI 函数以执行这些操作。这称为 punting 到 GDI。 在某些情况下，必须在驱动程序中实现操作。 例如，如果驱动程序实现设备管理的图面，则必须在显示驱动程序中实现某些绘图函数。

### <a name="span-idhookingspanspan-idhookingspanspan-idhookingspanhooking"></a><span id="Hooking"></span><span id="hooking"></span><span id="HOOKING"></span>挂接

默认情况下，当绘图图面为引擎管理的图面时，GDI 将处理绘图 (呈现) 操作。 为了使驱动程序能够利用为给定表面的部分或全部绘图功能提供加速的硬件，或使用特殊的块传输硬件，它可以挂钩这些功能。 为了挂钩调用，驱动程序将挂钩指定为[**EngAssociateSurface**](/windows/win32/api/winddi/nf-winddi-engassociatesurface)和[**EngModifySurface**](/windows/win32/api/winddi/nf-winddi-engmodifysurface)函数的*flHook*参数的标志。

如果驱动程序指定函数的挂钩标志，则它必须在支持的图形 DDI 入口点列表中提供该函数。 驱动程序可以优化硬件支持的操作。 此类驱动程序可能只处理挂钩调用上的某些事例。 例如，如果在挂钩的调用上请求复杂的图形，则可能仍会更有效地指出对 GDI 的回调，从而允许 GDI 处理操作。

下面是选择是否处理挂钩调用的驱动程序的另一个示例。 假设有一个驱动程序，该驱动程序支持能够处理某些 *ROPs*的位块传输调用的硬件。 即使此驱动程序可以自行执行许多操作，它也只是帧缓冲区。 此类驱动程序会将帧缓冲区的位图表面的句柄返回为其 *PDEV*的图面，但会将 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt) 调用挂钩到其自身。 当 GDI 调用 *DrvBitBlt*时，驱动程序可以检查 ROP，以查看它是否为硬件支持的一个。 否则，驱动程序可以通过调用 [**EngBitBlt**](/windows/win32/api/winddi/nf-winddi-engbitblt) 函数将操作传递回 GDI。

支持设备托管的图面的驱动程序必须挂接一些绘图函数;即 [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits)、 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout)和 [**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath)。 尽管 GDI 模拟可以处理其他的绘制函数，但出于性能原因，此类型的驱动程序需要挂钩其他函数（如 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt) 和 [**DrvRealizeBrush**](/windows/win32/api/winddi/nf-winddi-drvrealizebrush) 函数），因为模拟需要从图面绘制和到图面。

### <a name="span-idpuntingspanspan-idpuntingspanspan-idpuntingspanpunting"></a><span id="Punting"></span><span id="punting"></span><span id="PUNTING"></span>Punting

*Punting* 对 gdi 的回调意味着要放入对相应 GDI 模拟的调用。 通常，对于每个 *DrvXxx* 图形调用，都有相应的 GDI **Eng ** * * Xxx 模拟调用，该调用采用相同的参数。 只要驱动程序已使位图 nonopaque，就可以在不更改 GDI 模拟的情况下传递所有参数。 对于每次调用 punts，驱动程序的大小都会降低 (因为该功能的代码可以) 省略。 但是，由于引擎拥有调用，因此驱动程序无法控制执行速度。 在某些复杂情况下，在驱动程序中提供支持时可能没有真正的优势。

### <a name="span-idhookable_gdi_graphics_output_functionsspanspan-idhookable_gdi_graphics_output_functionsspanspan-idhookable_gdi_graphics_output_functionsspanhookable-gdi-graphics-output-functions"></a><span id="Hookable_GDI_Graphics_Output_Functions"></span><span id="hookable_gdi_graphics_output_functions"></span><span id="HOOKABLE_GDI_GRAPHICS_OUTPUT_FUNCTIONS"></span>延展 GDI 图形输出函数

下表列出了驱动程序可以挂钩的图形输出函数和相应的 GDI 模拟功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序图形输出函数</th>
<th align="left">对应的 GDI 模拟</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvbitblt)"><strong>DrvBitBlt</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engbitblt" data-raw-source="[&lt;strong&gt;EngBitBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engbitblt)"><strong>EngBitBlt</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvplgblt)"><strong>DrvPlgBlt</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engplgblt" data-raw-source="[&lt;strong&gt;EngPlgBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engplgblt)"><strong>EngPlgBlt</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstretchblt)"><strong>DrvStretchBlt</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engstretchblt" data-raw-source="[&lt;strong&gt;EngStretchBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engstretchblt)"><strong>EngStretchBlt</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstretchbltrop)"><strong>DrvStretchBltROP</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engstretchbltrop" data-raw-source="[&lt;strong&gt;EngStretchBltROP&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engstretchbltrop)"><strong>EngStretchBltROP</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvtextout" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvtextout)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engtextout" data-raw-source="[&lt;strong&gt;EngTextOut&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engtextout)"><strong>EngTextOut</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstrokepath" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstrokepath)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engstrokepath" data-raw-source="[&lt;strong&gt;EngStrokePath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engstrokepath)"><strong>EngStrokePath</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvfillpath)"><strong>DrvFillPath</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engfillpath" data-raw-source="[&lt;strong&gt;EngFillPath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engfillpath)"><strong>EngFillPath</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvstrokeandfillpath)"><strong>DrvStrokeAndFillPath</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engstrokeandfillpath" data-raw-source="[&lt;strong&gt;EngStrokeAndFillPath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engstrokeandfillpath)"><strong>EngStrokeAndFillPath</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvlineto)"><strong>DrvLineTo</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-englineto" data-raw-source="[&lt;strong&gt;EngLineTo&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-englineto)"><strong>EngLineTo</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvcopybits" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvcopybits)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcopybits" data-raw-source="[&lt;strong&gt;EngCopyBits&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcopybits)"><strong>EngCopyBits</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvalphablend)"><strong>DrvAlphaBlend</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engalphablend" data-raw-source="[&lt;strong&gt;EngAlphaBlend&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engalphablend)"><strong>EngAlphaBlend</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvgradientfill)"><strong>DrvGradientFill</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-enggradientfill" data-raw-source="[&lt;strong&gt;EngGradientFill&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-enggradientfill)"><strong>EngGradientFill</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvtransparentblt)"><strong>DrvTransparentBlt</strong></a></p></td>
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engtransparentblt" data-raw-source="[&lt;strong&gt;EngTransparentBlt&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engtransparentblt)"><strong>EngTransparentBlt</strong></a></p></td>
</tr>
</tbody>
</table>

 

