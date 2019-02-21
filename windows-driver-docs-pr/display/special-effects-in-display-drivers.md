---
title: 显示驱动程序中的特殊效果
description: 显示驱动程序中的特殊效果
ms.assetid: f44a89df-6412-442c-8491-3e2f2bbd826f
keywords:
- 显示驱动程序 WDK Windows 2000 中，特殊效果
- 特殊效果 WDK Windows 2000 显示
- 显示效果 WDK Windows 2000
- 显示 blend 中动画 WDK Windows 2000
- 显示 blend 扩展动画 WDK Windows 2000
- alpha 游标 WDK Windows 2000 显示
- 显示渐变填充 WDK Windows 2000
- alpha 值混合处理 WDK Windows 2000 显示
- 位块传输 WDK Windows 2000 显示
- 拉伸 WDK Windows 2000 显示
- 显示动画 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3390248bdfc81aba6604f2abe79d7cd395d99bfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525577"
---
# <a name="special-effects-in-display-drivers"></a>显示驱动程序中的特殊效果


## <span id="ddk_special_effects_in_display_drivers_gg"></span><span id="DDK_SPECIAL_EFFECTS_IN_DISPLAY_DRIVERS_GG"></span>


Windows 2000 和更高版本的操作系统版本支持以下特殊效果：

-   如果显示硬件支持 alpha 值混合处理，显示器驱动程序，可以实现[ **DrvAlphaBlend**](https://msdn.microsoft.com/library/windows/hardware/ff556176)。

-   如果显示硬件支持渐变填充，显示器驱动程序应实现[ **DrvGradientFill**](https://msdn.microsoft.com/library/windows/hardware/ff556236)。

### <a name="span-idalphablendingspanspan-idalphablendingspanspan-idalphablendingspanalpha-blending"></a><span id="Alpha_Blending"></span><span id="alpha_blending"></span><span id="ALPHA_BLENDING"></span>Alpha 值混合处理

Microsoft Windows 2000 （和更高版本） Shell alpha 值混合处理大量使用以执行操作，如*blend 中*并*blend 扩展动画*并*alpha 游标*。 Alpha 混合操作需要读取的源和目标的图面，因为它是非常慢时位于视频内存中的源或目标到 GDI 稍作。 因此，驱动程序中的硬件加速功能将产生以可视方式更流畅的动画而提高系统整体性能。

驱动程序应实现**DrvAlphaBlend**，前提是没有接缝是曾经可见。

通过生成最坏的情况的错误*DrvAlphaBlend*不应超过一 (1) 每个颜色通道。 源时涉及拉伸，则应该在混合; 之前是 COLORONCOLOR 拉伸 （请参阅 Windows SDK 文档）最坏的情况的错误不应超过一 (1) 每个颜色通道结合使用，最坏的情况延伸错误。

Alpha 值混合处理具有拉伸组合的情况下，在有 WDK，其计算结果的显示驱动程序的实现中的测试*DrvAlphaBlend*如下所示：

1.  测试调用显示器驱动程序*DrvAlphaBlend*，生成一个 alpha 混合和拉伸的矩形。

2.  测试生成目标矩形，与所用对的调用中使用相同的源矩形*DrvAlphaBlend*。

3.  每个像素 P 的目标矩形的步骤 2 中，测试将模拟为反向拉伸来拉伸之前确定源矩形中的相应像素。 测试适用于反向拉伸以适应不同的拉伸实现由驱动程序容差值。 测试然后计算应应用于该像素的 alpha 混合。

    因为任何四个可能像素 （角的 3 个像素方形像素 P 上居中） 在源中矩形无法拉伸以产生像素 P 的目标矩形中，测试必须比较每个角像素的颜色值与在第像素e 的矩形中的相应位置由*DrvAlphaBlend*。

最坏的情况延伸错误是颜色值中的相应角像素，其中一个位于任何对之间的最大区别*DrvAlphaBlend*-生成矩形，并且另一种是在测试生成的源矩形。

### <a name="span-idgradientfillsspanspan-idgradientfillsspanspan-idgradientfillsspangradient-fills"></a><span id="Gradient_Fills"></span><span id="gradient_fills"></span><span id="GRADIENT_FILLS"></span>渐变填充

使用 Windows 2000 （和更高版本） 外壳*渐变填充*所有标题栏。

生成的结果[ **DrvGradientFill** ](https://msdn.microsoft.com/library/windows/hardware/ff556236)取决于每像素的比特数，且必须满足以下准则：

### <a name="span-id24bppor32bppsurfacesspanspan-id24bppor32bppsurfacesspan24-bpp-or-32-bpp-surfaces"></a><span id="_24_bpp_or_32_bpp_surfaces"></span><span id="_24_BPP_OR_32_BPP_SURFACES"></span>24 bpp 或 32 bpp 应用层

-   值必须增加或减少单调 gradated 的所有方向。

-   矩形渐变：当*ulMode* = = 渐变\_填充\_RECT\_H，每个垂直条必须是一种颜色。
    当*ulMode* = = 渐变\_填充\_RECT\_V，每个水平条必须是一种颜色。
-   任何通道内最坏的情况的错误不能超过 Â±1。

-   区域的终结点必须是完全匹配项。

### <a name="span-id15bppor16bppsurfacesspanspan-id15bppor16bppsurfacesspan15-bpp-or-16-bpp-surfaces"></a><span id="_15_bpp_or_16_bpp_surfaces"></span><span id="_15_BPP_OR_16_BPP_SURFACES"></span>15-bpp 或 16 bpp 应用层

任何通道内最坏的情况的错误不能超过 Â±15。

### <a name="span-id1bppto8bppsurfacesspanspan-id1bppto8bppsurfacesspan1-bpp-to-8-bpp-surfaces"></a><span id="_1_bpp_to_8_bpp_surfaces"></span><span id="_1_BPP_TO_8_BPP_SURFACES"></span>1-bpp 到 8 bpp 表面

渐变填充任何这些图面中不允许存在任何错误。 对于 8 bpp 曲面，GDI 不会调用驱动程序的*DrvGradientFill*函数。

请注意，在所有图面，剪辑不会影响结果。

 

 





