---
title: 显示驱动程序中的特效
description: 显示驱动程序中的特效
keywords:
- 显示驱动程序 WDK Windows 2000，特殊效果
- 特殊效果 WDK Windows 2000 显示
- 效果 WDK Windows 2000 显示
- 融合动画 WDK Windows 2000 显示
- 融合动画 WDK Windows 2000 显示
- alpha 光标 WDK Windows 2000 显示
- 渐变填充 WDK Windows 2000 显示
- alpha 混合 WDK Windows 2000 显示器
- 位块传输 WDK Windows 2000 显示器
- 拉伸 WDK Windows 2000 显示器
- 动画 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc5c1f2498ea874478387cd8a1308f89bce6d5f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837797"
---
# <a name="special-effects-in-display-drivers"></a>显示驱动程序中的特效


## <span id="ddk_special_effects_in_display_drivers_gg"></span><span id="DDK_SPECIAL_EFFECTS_IN_DISPLAY_DRIVERS_GG"></span>


Windows 2000 及更高版本的操作系统版本支持以下特殊效果：

-   如果显示硬件支持 alpha 混合，则显示驱动程序可以实现 [**DrvAlphaBlend**](/windows/win32/api/winddi/nf-winddi-drvalphablend)。

-   如果显示硬件支持渐变填充，则显示驱动程序应实现 [**DrvGradientFill**](/windows/win32/api/winddi/nf-winddi-drvgradientfill)。

### <a name="span-idalpha_blendingspanspan-idalpha_blendingspanspan-idalpha_blendingspanalpha-blending"></a><span id="Alpha_Blending"></span><span id="alpha_blending"></span><span id="ALPHA_BLENDING"></span>Alpha 混合

Microsoft Windows 2000 (及更高版本) Shell 会广泛使用 alpha 混合来执行 *混合* 、 *混合动画* 和 *alpha 光标* 等操作。 由于 alpha blend 运算需要从源和目标面中进行读取，因此当源或目标位于视频内存中时，会很慢地出现 GDI。 因此，驱动程序中的硬件加速将生成明显更流畅的动画，并改善系统的整体性能。

驱动程序应使用常量 alpha 和 32 bpp BGRA 系统内存区中的 *位块传输* 来实现 [**DrvAlphaBlend**](/windows/win32/api/winddi/nf-winddi-drvalphablend) ，并使用每像素的 alpha 值。 如果看不到任何接缝，则可以使用 *三角形纹理填充* 来实现 *DrvAlphaBlend* 。

*DrvAlphaBlend* 生成的最坏情况错误不应超过每个颜色通道一 (1) 。 当涉及拉伸时，应将源 COLORONCOLOR 拉伸 (在混合之前查看 Windows SDK 文档) ;最坏情况错误不应超过每个颜色通道) 一个 (1 与最差的 "拉伸" 错误组合。

在 alpha 混合与拉伸结合使用的情况下，WDK 中的测试会按以下方式评估显示器驱动程序的 *DrvAlphaBlend* 实现：

1.  该测试将调用显示器驱动程序的 *DrvAlphaBlend*，从而生成一个 alpha 混合矩形。

2.  测试将使用与对 *DrvAlphaBlend* 的调用中使用的相同源矩形生成目标矩形。

3.  对于步骤2的目标矩形中的每个象素 P，该测试会模拟反向拉伸，以在拉伸之前确定源矩形中的相应像素。 该测试将公差值应用于反向拉伸，以适应驱动程序的不同 stretch 实现。 然后，测试计算应该应用于该像素的 alpha blend。

    由于四个可能的像素 (在源矩形中) 居中的 3 X 3 像素正方形的角可能会拉伸以在目标矩形中产生像素 P，因此，该测试必须将每个角像素的颜色值与 *DrvAlphaBlend* 生成的矩形中相应位置的像素的颜色值进行比较。

最坏情况下，拉伸错误是任意一对角像素之间颜色值的最大差值，其中其中一个像素位于 *DrvAlphaBlend* 生成的矩形上，另一个位于测试生成的源矩形上。

### <a name="span-idgradient_fillsspanspan-idgradient_fillsspanspan-idgradient_fillsspangradient-fills"></a><span id="Gradient_Fills"></span><span id="gradient_fills"></span><span id="GRADIENT_FILLS"></span>渐变填充

Windows 2000 (及更高版本) Shell 对所有标题栏使用 *渐变填充* 。

[**DrvGradientFill**](/windows/win32/api/winddi/nf-winddi-drvgradientfill)产生的结果取决于每个像素的位数，并且必须满足以下准则：

### <a name="span-id_24_bpp_or_32_bpp_surfacesspanspan-id_24_bpp_or_32_bpp_surfacesspan24-bpp-or-32-bpp-surfaces"></a><span id="_24_bpp_or_32_bpp_surfaces"></span><span id="_24_BPP_OR_32_BPP_SURFACES"></span>24-bpp 或 32-bpp 面

-   值必须在所有 gradated 方向上按单调增加或减少。

-   对于矩形渐变：当 *ulMode* = = 渐变 \_ 填充 \_ 矩形 \_ H 时，每个垂直条必须是一种颜色。
    当 *ulMode* = = 梯度 \_ 填充 \_ RECT \_ V 时，每个水平条必须是一种颜色。
-   任何通道中的最差案例错误不能超过±1。

-   区域的终结点必须完全匹配。

### <a name="span-id_15_bpp_or_16_bpp_surfacesspanspan-id_15_bpp_or_16_bpp_surfacesspan15-bpp-or-16-bpp-surfaces"></a><span id="_15_bpp_or_16_bpp_surfaces"></span><span id="_15_BPP_OR_16_BPP_SURFACES"></span>15-bpp 或 16 bpp 面

任何通道中的最差案例错误不能超过±15。

### <a name="span-id_1_bpp_to_8_bpp_surfacesspanspan-id_1_bpp_to_8_bpp_surfacesspan1-bpp-to-8-bpp-surfaces"></a><span id="_1_bpp_to_8_bpp_surfaces"></span><span id="_1_BPP_TO_8_BPP_SURFACES"></span>1-bpp 到 8-bpp 面

对于任何这些图面，渐变填充不允许出错。 对于 8 bpp 面，GDI 不会调用驱动程序的 *DrvGradientFill* 函数。

请注意，在所有图面中，剪辑不会影响结果。

