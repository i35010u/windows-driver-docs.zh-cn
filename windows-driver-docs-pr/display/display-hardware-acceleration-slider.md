---
title: 显示硬件加速滑块
description: 显示硬件加速滑块
ms.assetid: af3daa64-196a-4163-872d-713bc4cf0335
keywords:
- 显示驱动程序 WDK Windows 2000 中，调试
- 显示调试驱动程序 WDK Windows 2000
- 硬件加速滑块 WDK Windows 2000 显示
- 加速滑块 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2944969d1aea7a719ca5f80dc38a3d1e9da1d4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385194"
---
# <a name="display-hardware-acceleration-slider"></a>显示硬件加速滑块


## <span id="ddk_display_hardware_acceleration_slider_gg"></span><span id="DDK_DISPLAY_HARDWARE_ACCELERATION_SLIDER_GG"></span>


**显示属性**对话框具有硬件加速滑块，它们可以帮助您调试显示器驱动程序。 通过使用滑块，可以设置显示硬件加速支持为到级别 5 （没有加速） 范围内的级别 0 （完全加速） 的六个级别之一。

若要查找 Microsoft Windows XP 硬件加速滑块，打开**显示属性**对话框中，单击**设置**选项卡。单击**高级**按钮，然后依次**疑难解答**选项卡。

以下列表介绍在每个级别禁用硬件加速的一部分。 所有后续级别禁用特定级别禁用任何功能。

<span id="Level_0"></span><span id="level_0"></span><span id="LEVEL_0"></span>**级别 0**  
滑块位于最右侧的位置。 完全启用硬件加速。

<span id="Level_1"></span><span id="level_1"></span><span id="LEVEL_1"></span>**级别 1**  
禁用硬件设备位图并游标支持。

<span id="Level_2"></span><span id="level_2"></span><span id="LEVEL_2"></span>**级别 2**  
以下显示驱动程序函数不会调用。 相反，GDI 中软件执行操作。

-   [**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)

-   [**DrvPlgBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)

-   [**DrvFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)

-   [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)

-   [**DrvLineTo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)

-   [**DrvStretchBltROP**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)

-   [**DrvTransparentBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)

-   [**DrvAlphaBlend**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)

-   [**DrvGradientFill**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)

<span id="Level_3"></span><span id="level_3"></span><span id="LEVEL_3"></span>**级别 3**  
禁用 Microsoft DirectDraw 和 Direct3D 支持。

<span id="Level_4"></span><span id="level_4"></span><span id="LEVEL_4"></span>**级别 4**  
只能将以下图形操作，因此可以缩短。

-   [**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)

-   [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)

-   [**DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)

-   [**DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)

此外，不会调用以下显示驱动程序函数。

-   [**DrvSaveScreenBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsavescreenbits)

-   [**DrvEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)

-   [**DrvDrawEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape)

-   [**DrvResetPDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)

-   [**DrvSetPixelFormat**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)

-   [**DrvDescribePixelFormat**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat)

-   [**DrvSwapBuffers**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers)

<span id="Level_5"></span><span id="level_5"></span><span id="LEVEL_5"></span>**级别 5**  
滑块位于最左侧的位置。 平移的驱动程序 （内核模式 GDI 的一部分） 将处理所有呈现。 GDI 调用显示器驱动程序[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)并[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)函数以创建主图面，同时调用若要设置的显示模式显示驱动程序。 显示驱动程序不调用以执行任何呈现。

限制显示硬件加速另一种方法是在中设置标志**CapabilityOverride**注册表项。 例如，设置 0x2 标志**CapabilityOverride**条目相当于将硬件加速滑块放在级别 3。 有关的说明**CapabilityOverride**注册表项，请参阅[显示 INF 文件部分](display-inf-file-sections.md)。

 

 





