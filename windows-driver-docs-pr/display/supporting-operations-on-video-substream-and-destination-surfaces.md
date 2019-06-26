---
title: 针对视频子流和目标图面的操作
description: VMR Microsoft Windows Server 2003 SP1 及更高版本和 Windows XP SP2 和更高版本必须能够执行视频子流和目标的图面上进行某些操作。
ms.assetid: ad0214b9-5d75-455f-8748-ff7c5a3d89db
keywords:
- DeinterlaceBltEx，目标图面
- DeinterlaceBltEx，子流图面
- 目标的图面 WDK DirectX VA
- 子流图面 WDK DirectX VA
- 颜色填充目标显示 WDK DirectX VA
- 颜色填充子流图面 WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: fbadc4d44feed8cc8638c46ff7aadc4610c82a1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380531"
---
# <a name="operations-on-video-substream-and-destination-surfaces"></a>针对视频子流和目标图面的操作


## <span id="ddk_supporting_operations_on_video_substream_and_destination_surfaces_"></span><span id="DDK_SUPPORTING_OPERATIONS_ON_VIDEO_SUBSTREAM_AND_DESTINATION_SURFACES_"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

VMR Microsoft Windows Server 2003 SP1 及更高版本和 Windows XP SP2 和更高版本必须能够执行视频子流和目标的图面上进行某些操作。

### <a name="span-idoperationsonvideosubstreamsurfacesspanspan-idoperationsonvideosubstreamsurfacesspanspan-idoperationsonvideosubstreamsurfacesspanoperations-on-video-substream-surfaces"></a><span id="Operations_on_Video_Substream_Surfaces"></span><span id="operations_on_video_substream_surfaces"></span><span id="OPERATIONS_ON_VIDEO_SUBSTREAM_SURFACES"></span>视频子流图面上的操作

除了视频子流上的操作显示您的驱动程序[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)并[ **DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)函数执行，您的驱动程序必须支持以下操作：

<span id="Color_Filling_Substream_Surfaces"></span><span id="color_filling_substream_surfaces"></span><span id="COLOR_FILLING_SUBSTREAM_SURFACES"></span>**颜色填充子流图面**  
VMR 和其他 Microsoft DirectShow 组件必须能够以填充为已知的初始颜色值，如透明的黑色的视频子流图面。 因此，您的驱动程序应支持对调用其[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)回调函数使用 DDBLT\_COLORFILL 标志视频子流图面所在的目标位块传输 （blt)。

对于视频子流图面与 AYUV *FOURCC*格式，VMR 指定透明黑色墨水 AYUV 颜色**dwFillColor** DDBLTFX 结构中的成员。 驱动程序收到中的 DDBLTFX **bltFX** DD 成员\_BLTDATA 结构时其*DdBlt*调用函数。 DDBLTFX 结构有关的信息，请参阅 Windows SDK 文档。

透明的黑色的 AYUV 颜色设置，如下所示：

```cpp
DXVA_AYUVsample2 clr; 
clr.bCrValue = 0x80;
clr.bCbValue = 0x80;
clr.bY_Value = 0x10;
clr.bSampleAlpha8 = 0x00;
DWORD dwFillColor = *(DWORD*)&clr;
```

对于使用 AI44 或 IA44 格式中的值的低序位字节视频子流图面**dwFillColor**成员指示驱动程序应使用以填充表面的颜色值。 通常情况下，颜色值为 0。

<span id="Copying_Contents_to_Substream_Surfaces"></span><span id="copying_contents_to_substream_surfaces"></span><span id="COPYING_CONTENTS_TO_SUBSTREAM_SURFACES"></span>**将内容复制到子流图面**  
Line21 关闭标题解码器和 teletext 解码器创建包含一系列缓存字符标志符号的源视频的子流图面。 通过将适当字符标志符号缓存中复制到视频子流图面，您的驱动程序应生成输出的每个帧。 VMR 然后向您的驱动程序发送视频子流图面[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)函数。

因此，您的驱动程序的[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)函数应支持将任何 FOURCC 面复制到相同的 FOURCC 格式的视频子流图面。

您的驱动程序应指示它通过设置 DDCAPS2 支持复制 FOURCC 格式\_COPYFOURCC 标志**dwCaps2**的成员[ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构。 该驱动程序指定 DDCORECAPS 结构中的**ddCaps**的成员[ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构。 DD\_驱动程序的返回 HALINFO [ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)函数。

在 FOURCC 视频子流图面上的复制操作中，该驱动程序不应执行拉伸或颜色空间转换操作。

### <a name="span-idoperationsondestinationsurfacesspanspan-idoperationsondestinationsurfacesspanspan-idoperationsondestinationsurfacesspanoperations-on-destination-surfaces"></a><span id="Operations_on_Destination_Surfaces"></span><span id="operations_on_destination_surfaces"></span><span id="OPERATIONS_ON_DESTINATION_SURFACES"></span>目标图面上的操作

您的驱动程序必须在您的驱动程序支持以下操作上使用的目标面[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)函数：

<span id="Color_Filling_the_Destination_Surface"></span><span id="color_filling_the_destination_surface"></span><span id="COLOR_FILLING_THE_DESTINATION_SURFACE"></span>**填充目标表面的颜色**  
因为 VMR 必须初始化到 YUV 不透明的黑色，您的驱动程序必须在目标面还支持调用其[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)回调函数使用 DDBLT\_COLORFILL 标记的位置位块传输的目标是目标图面。 VMR 指定的不透明黑色墨水颜色**dwFillColor** DDBLTFX 结构中的成员。 该驱动程序接收中的 DDBLTFX 结构**bltFX** DD 成员\_BLTDATA 结构时其*DdBlt*调用。

为图面类型打包的 YUV，VMR 将 DWORD 的填充颜色设置为不透明的黑色的相应字节模式。 YUY2 图面，为不透明的黑色的填充颜色 DWORD 是 0x80108010。

对于平面数据图面上的类型，VMR，如下所示设置不透明的黑色的 AYUV 颜色：

```cpp
DXVA_AYUVsample2 clr; 
clr.bCrValue = 0x80;
clr.bCbValue = 0x80;
clr.bY_Value = 0x10;
clr.bSampleAlpha8 = 0xFF;
DWORD dwFillColor = *(DWORD*)&clr;
```

您的驱动程序应确保正确的像素值将写入每个平面 YUV 图面。

<span id="Stretching_the_Destination_Surface"></span><span id="stretching_the_destination_surface"></span><span id="STRETCHING_THE_DESTINATION_SURFACE"></span>**拉伸目标面**  
您的驱动程序还必须支持目标表面用作组合颜色空间转换的延伸操作位块传输源图面。 有关详细信息，请参阅[支持 Stretch 位块操作](supporting-stretch-blit-operations.md)。

<span id="Copying_Contents_from_the_Destination_Surface"></span><span id="copying_contents_from_the_destination_surface"></span><span id="COPYING_CONTENTS_FROM_THE_DESTINATION_SURFACE"></span>**目标图面中复制的内容**  
您的驱动程序*DdBlt*函数必须支持复制到相同的 FOURCC 格式的面 FOURCC 目标图面。 目标面用作复制操作中的源图面。 您的驱动程序应指示它通过设置 DDCAPS2 支持复制 FOURCC 格式\_COPYFOURCC 标志。

位块传输操作的目标面可以是主图面或 Direct3D 纹理。

 

 





