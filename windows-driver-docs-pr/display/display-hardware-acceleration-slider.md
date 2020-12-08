---
title: 显示硬件加速滑块
description: 显示硬件加速滑块
keywords:
- 显示驱动程序 WDK Windows 2000，调试
- 调试驱动程序 WDK Windows 2000 显示
- 硬件加速滑块 WDK Windows 2000 显示
- 加速滑块 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ea15bd65ef5da17c5869a487248f7ee98037ed9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809251"
---
# <a name="display-hardware-acceleration-slider"></a>显示硬件加速滑块


## <span id="ddk_display_hardware_acceleration_slider_gg"></span><span id="DDK_DISPLAY_HARDWARE_ACCELERATION_SLIDER_GG"></span>


" **显示属性** " 对话框中有一个 "硬件加速" 滑块，当您调试显示驱动程序时，此滑块非常有用。 通过使用滑块，你可以将 "显示硬件加速支持" 设置为以下六个级别之一：从级别 0 ("完全加速") 到 "级别 5" ("无加速) "。

若要在 Microsoft Windows XP 中查找硬件加速滑块，请打开 " **显示属性** " 对话框，然后单击 " **设置** " 选项卡。单击 " **高级** " 按钮，然后单击 " **疑难解答** " 选项卡。

以下列表描述了每个级别禁用的硬件加速部分。 在特定级别禁用的任何功能在所有后续级别中都处于禁用状态。

<span id="Level_0"></span><span id="level_0"></span><span id="LEVEL_0"></span>**级别0**  
滑块位于最右侧位置。 完全启用硬件加速。

<span id="Level_1"></span><span id="level_1"></span><span id="LEVEL_1"></span>**级别1**  
硬件光标和设备位图支持已禁用。

<span id="Level_2"></span><span id="level_2"></span><span id="LEVEL_2"></span>**级别2**  
不会调用以下显示驱动程序函数。 GDI 将在软件中执行这些操作。

-   [**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt)

-   [**DrvPlgBlt**](/windows/win32/api/winddi/nf-winddi-drvplgblt)

-   [**DrvFillPath**](/windows/win32/api/winddi/nf-winddi-drvfillpath)

-   [**DrvStrokeAndFillPath**](/windows/win32/api/winddi/nf-winddi-drvstrokeandfillpath)

-   [**DrvLineTo**](/windows/win32/api/winddi/nf-winddi-drvlineto)

-   [**DrvStretchBltROP**](/windows/win32/api/winddi/nf-winddi-drvstretchbltrop)

-   [**DrvTransparentBlt**](/windows/win32/api/winddi/nf-winddi-drvtransparentblt)

-   [**DrvAlphaBlend**](/windows/win32/api/winddi/nf-winddi-drvalphablend)

-   [**DrvGradientFill**](/windows/win32/api/winddi/nf-winddi-drvgradientfill)

<span id="Level_3"></span><span id="level_3"></span><span id="LEVEL_3"></span>**级别3**  
Microsoft DirectDraw 和 Direct3D 支持已禁用。

<span id="Level_4"></span><span id="level_4"></span><span id="LEVEL_4"></span>**级别4**  
仅加速了以下图形操作。

-   [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout)

-   [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)

-   [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits)

-   [**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath)

此外，不会调用以下显示驱动程序函数。

-   [**DrvSaveScreenBits**](/windows/win32/api/winddi/nf-winddi-drvsavescreenbits)

-   [**DrvEscape**](/windows/win32/api/winddi/nf-winddi-drvescape)

-   [**DrvDrawEscape**](/windows/win32/api/winddi/nf-winddi-drvdrawescape)

-   [**DrvResetPDEV**](/windows/win32/api/winddi/nf-winddi-drvresetpdev)

-   [**DrvSetPixelFormat**](/windows/win32/api/winddi/nf-winddi-drvsetpixelformat)

-   [**DrvDescribePixelFormat**](/windows/win32/api/winddi/nf-winddi-drvdescribepixelformat)

-   [**DrvSwapBuffers**](/windows/win32/api/winddi/nf-winddi-drvswapbuffers)

<span id="Level_5"></span><span id="level_5"></span><span id="LEVEL_5"></span>**级别5**  
滑块位于最左侧位置。 平移驱动程序 (内核模式 GDI) 的一部分处理所有呈现。 GDI 调用显示器驱动程序的 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 和 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数来创建主表面，还会调用显示器驱动程序来设置显示模式。 不会调用显示驱动程序来执行任何呈现。

限制显示硬件加速的另一种方法是在 **CapabilityOverride** 注册表项中设置标志。 例如，在 " **CapabilityOverride** " 项中设置0x2 标志等效于将 "硬件加速" 滑块置于第3级。 有关 **CapabilityOverride** 注册表项的说明，请参阅 [显示 INF 文件部分](display-inf-file-sections.md)。

 

