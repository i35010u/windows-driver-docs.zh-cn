---
title: 报告 DeinterlaceBltEx 支持
description: 报告 DeinterlaceBltEx 支持
ms.assetid: 9cf8d05c-ef59-44a4-a377-66282e7888d5
keywords:
- DeinterlaceBltEx，报表
- DXVA_VideoProcess_SubStreamsExtended
- DXVA_VideoProcess_YUV2RGBExtended
- DXVA_VideoProcess_AlphaBlendExtended
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce6493015df036872e29e759f4a5735dbf929fe8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829589"
---
# <a name="reporting-support-for-deinterlacebltex"></a>报告 DeinterlaceBltEx 支持


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

显示驱动程序通过设置 DXVA\_VideoProcess\_SubStreams、DXVA\_VideoProcess\_StretchX 和 DXVA\_VideoProcess 来报告对[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)取消[隔行执行 DDI](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-ddi)函数的支持 @no__[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的**VideoProcessingCaps**成员中的 t_8_ 伸缩标志。 调用[**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)函数时，驱动程序将返回指向 DXVA\_DeinterlaceCaps 的指针。

显示驱动程序将 DXVA\_VideoProcess\_SubStreams 设置为结合取消隔行扫描的视频子流组合。 该驱动程序将 DXVA\_VideoProcess\_StretchX 和 DXVA\_VideoProcess\_伸缩，因为视频流和 substreams 的像素纵横比可能不同且不为，并且驱动程序必须能够独立地拉伸（水平和/或垂直）为取消隔行扫描提交的视频帧以及提供的视频 substreams。

[**VideoProcess\_AlphaBlend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的**VideoProcessingCaps**成员中的 DXVA\_VIDEOPROCESS\_YUV2RGB 和 DXVA\_DXVA\_DeinterlaceCaps 标志在该驱动程序的上下文中没有意义[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)函数。 这些标志与原始[**DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)函数相关。 由于支持*DeinterlaceBltEx*的显示驱动程序还必须支持*DeinterlaceBlt*，因此，如果驱动程序在*DeinterlaceBlt*的上下文中支持其关联的操作，则该驱动程序仍必须报告这些标志。

### <a name="span-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspanspan-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspanspan-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspandxva_videoprocess_substreamsextended-dxva_videoprocess_yuv2rgbextended-and-dxva_videoprocess_alphablendextended-flags"></a><span id="DXVA_VideoProcess_SubStreamsExtended_DXVA_VideoProcess_YUV2RGBExtended_and_DXVA_VideoProcess_AlphaBlendExtended_flags"></span><span id="dxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flags"></span><span id="DXVA_VIDEOPROCESS_SUBSTREAMSEXTENDED_DXVA_VIDEOPROCESS_YUV2RGBEXTENDED_AND_DXVA_VIDEOPROCESS_ALPHABLENDEXTENDED_FLAGS"></span>DXVA\_VideoProcess\_SubStreamsExtended DXVA\_VideoProcess\_YUV2RGBExtended 和 DXVA\_VideoProcess\_AlphaBlendExtended 标志

实现[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)函数的显示驱动程序可以为每个源和目标图面支持明显增强的颜色信息。 该驱动程序可以通过设置 DXVA\_VideoProcess\_SubStreamsExtended、DXVA\_VideoProcess\_YUV2RGBExtended 和 DXVA\_VideoProcess 中的**AlphaBlendExtended 标志来报告此类支持VideoProcessingCaps** [**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的成员。

支持 DXVA\_VideoProcess\_SubStreamsExtended 标志指示显示驱动程序可以对源视频流和 substreams 执行所需的颜色调整。 这些调整会在扩展的颜色数据中指示，因为视频 deinterlaced，与 substreams 复合并写入目标图面。 扩展颜色数据由源示例数组的[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的**SampleFormat**成员中的[**DXVA\_ExtendedFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_extendedformat)结构的成员指定（*lpDDSrcSurfaces*[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)调用中的参数或[**DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)结构的**源**成员）。

对 DXVA\_VideoProcess\_YUV2RGBExtended 标志的支持表示显示驱动程序可以执行颜色空间转换操作，因为 deinterlaced 并将合成像素写入目标图面。 如果将 RGB 目标图面传递到显示器驱动程序，VMR 将确保每个颜色通道至少包含8位。 RGB 目标图面可以是屏幕外、纹理或 Direct3D 呈现器目标，或者是组合纹理和 Direct3D 呈现器目标表面类型。 即使使用了 RGB 目标图面，VMR 仍指定 YUV 颜色空间中的背景色参数。

支持 DXVA\_VideoProcess\_AlphaBlendExtended 标志指示在将 deinterlaced 和合成像素写入目标时，显示驱动程序可以执行与目标图面的 alpha 混合操作面的. 驱动程序必须根据[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)调用中*fAlpha*参数的 alpha 值处理背景色。 当 alpha 值为 1.0 f 时，将以不透明（无透明度）绘制背景色。 当 alpha 值为 0.0 f 时，不应绘制背景（透明）。

 

 





