---
title: 针对视频子流和目标图面的操作
description: Microsoft Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 必须能够对视频子流和目标表面执行某些操作。
ms.assetid: ad0214b9-5d75-455f-8748-ff7c5a3d89db
keywords:
- DeinterlaceBltEx，目标图面
- DeinterlaceBltEx，子流表面
- 目标图面 WDK DirectX VA
- 子流图面 WDK DirectX VA
- 颜色填充目标图面 WDK DirectX VA
- 颜色填充子流图面 WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: b1c672484ef232bef38872c5265921b9493374d6
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717456"
---
# <a name="operations-on-video-substream-and-destination-surfaces"></a>针对视频子流和目标图面的操作


## <span id="ddk_supporting_operations_on_video_substream_and_destination_surfaces_"></span><span id="DDK_SUPPORTING_OPERATIONS_ON_VIDEO_SUBSTREAM_AND_DESTINATION_SURFACES_"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

Microsoft Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 必须能够对视频子流和目标表面执行某些操作。

### <a name="span-idoperations_on_video_substream_surfacesspanspan-idoperations_on_video_substream_surfacesspanspan-idoperations_on_video_substream_surfacesspanoperations-on-video-substream-surfaces"></a><span id="Operations_on_Video_Substream_Surfaces"></span><span id="operations_on_video_substream_surfaces"></span><span id="OPERATIONS_ON_VIDEO_SUBSTREAM_SURFACES"></span>视频子流图面上的操作

除了视频子流上的操作图面上驱动程序的 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 和 [**DeinterlaceBlt**](./dxva-deinterlacebobdeviceclass-deinterlaceblt.md) 函数执行的操作，驱动程序必须支持以下操作：

<span id="Color_Filling_Substream_Surfaces"></span><span id="color_filling_substream_surfaces"></span><span id="COLOR_FILLING_SUBSTREAM_SURFACES"></span>**颜色填充子流图面**  
VMR 和其他 Microsoft DirectShow 组件必须能够将视频子流表面填充到已知的初始颜色值，如透明黑色。 因此，你的驱动程序应使用 DDBLT COLORFILL 标志支持对其 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 回调函数的调用， \_ 其中视频子流图面的目标为位块传输 (blt) 的目标。

对于 AYUV *FOURCC* 格式的视频子流图面，VMR 在 dwFillColor 结构的 **DDBLTFX** 成员中指定透明黑色的 AYUV 颜色。 **bltFX** \_ 当调用*DdBlt*函数时，驱动程序将在 DD BLTDATA 结构的 bltFX 成员中接收 DDBLTFX。 有关 DDBLTFX 结构的信息，请参阅 Windows SDK 文档。

透明黑色的 AYUV 颜色设置如下：

```cpp
DXVA_AYUVsample2 clr; 
clr.bCrValue = 0x80;
clr.bCbValue = 0x80;
clr.bY_Value = 0x10;
clr.bSampleAlpha8 = 0x00;
DWORD dwFillColor = *(DWORD*)&clr;
```

对于具有 AI44 或 IA44 格式的视频子流图面， **dwFillColor** 成员中值的低序位字节指示驱动程序应用于填充图面的颜色值。 通常，颜色值为0。

<span id="Copying_Contents_to_Substream_Surfaces"></span><span id="copying_contents_to_substream_surfaces"></span><span id="COPYING_CONTENTS_TO_SUBSTREAM_SURFACES"></span>**将内容复制到子流图面**  
Line21 隐藏式字幕解码器和 teletext 解码器创建包含一系列缓存字符标志符号的源视频子流图面。 驱动程序应通过将相应的字符从字形缓存复制到视频子流图面来生成每个输出帧。 然后，VMR 将视频子流表面发送到驱动程序的 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 函数。

因此，驱动程序的 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 函数应支持将任何 FOURCC 图面复制到相同 FOURCC 格式的视频子流表面。

驱动程序应指示它支持通过 \_ 在[**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**DWCAPS2**成员中设置 DDCAPS2 COPYFOURCC 标志来复制 FOURCC 格式。 驱动程序在[**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**DDCAPS**成员中指定 DDCORECAPS 结构。 DD \_ HALINFO 由驱动程序的 [**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo) 函数返回。

在 FOURCC 视频子流表面复制操作中，驱动程序不应执行拉伸或颜色空间转换操作。

### <a name="span-idoperations_on_destination_surfacesspanspan-idoperations_on_destination_surfacesspanspan-idoperations_on_destination_surfacesspanoperations-on-destination-surfaces"></a><span id="Operations_on_Destination_Surfaces"></span><span id="operations_on_destination_surfaces"></span><span id="OPERATIONS_ON_DESTINATION_SURFACES"></span>针对目标面的操作

您的驱动程序必须支持在您的驱动程序的 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 函数中使用的目标表面上执行以下操作：

<span id="Color_Filling_the_Destination_Surface"></span><span id="color_filling_the_destination_surface"></span><span id="COLOR_FILLING_THE_DESTINATION_SURFACE"></span>**填充目标图面的颜色**  
由于 VMR 必须将目标图面初始化为 YUV 不透明黑色，因此您的驱动程序还必须支持使用 DDBLT COLORFILL 标志调用其 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 回调函数， \_ 其中位块传输的目标是目标面。 VMR 指定 DDBLTFX 结构的 **dwFillColor** 成员中不透明黑色的颜色。 该驱动程序在调用 DdBlt 时，在 DD BLTDATA 结构的**bltFX**成员中接收 DDBLTFX 结构 \_ 。 *DdBlt*

对于 YUV 打包的图面类型，VMR 将填充颜色 DWORD 设置为适用于不透明黑色的适当字节模式。 对于 YUY2 表面，不透明黑色的填充颜色 DWORD 为0x80108010。

对于平面表面类型，VMR 设置不透明黑色的 AYUV 颜色，如下所示：

```cpp
DXVA_AYUVsample2 clr; 
clr.bCrValue = 0x80;
clr.bCbValue = 0x80;
clr.bY_Value = 0x10;
clr.bSampleAlpha8 = 0xFF;
DWORD dwFillColor = *(DWORD*)&clr;
```

您的驱动程序应确保将正确的像素值写入到 YUV 图面的每个平面。

<span id="Stretching_the_Destination_Surface"></span><span id="stretching_the_destination_surface"></span><span id="STRETCHING_THE_DESTINATION_SURFACE"></span>**拉伸目标图面**  
你的驱动程序还必须支持用作位块传输的源图面的位块传输的源图面，此操作组合拉伸操作和颜色空间转换。 有关详细信息，请参阅 [支持 Stretch Array.blit 操作](supporting-stretch-blit-operations.md)。

<span id="Copying_Contents_from_the_Destination_Surface"></span><span id="copying_contents_from_the_destination_surface"></span><span id="COPYING_CONTENTS_FROM_THE_DESTINATION_SURFACE"></span>**从目标图面复制内容**  
驱动程序的 *DdBlt* 函数必须支持将 FOURCC 目标图面复制到相同 FOURCC 格式的表面。 目标图面用作复制操作中的源图面。 驱动程序应指示它支持通过设置 DDCAPS2 COPYFOURCC 标志来复制 FOURCC 格式 \_ 。

位块传输操作的目标图面可以是主要表面或 Direct3D 纹理。

 

