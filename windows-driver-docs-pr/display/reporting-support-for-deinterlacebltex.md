---
title: 报告 DeinterlaceBltEx 支持
description: 报告 DeinterlaceBltEx 支持
keywords:
- DeinterlaceBltEx，报表
- DXVA_VideoProcess_SubStreamsExtended
- DXVA_VideoProcess_YUV2RGBExtended
- DXVA_VideoProcess_AlphaBlendExtended
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34f3ee27ede00ffe76c278160ac3e85f7bc7a236
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786873"
---
# <a name="reporting-support-for-deinterlacebltex"></a>报告 DeinterlaceBltEx 支持


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

显示驱动程序通过 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md)[deinterlace DDI](./deinterlace-ddi.md) \_ \_ \_ \_ \_ \_ 在 [**DXVA \_ VideoProcess**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的 **StretchX** 成员中设置 DXVA VideoProcess SubStreams、DXVA VideoProcess 伸缩和 VideoProcessingCaps DXVA DeinterlaceCaps 标志来报告对 DeinterlaceBltEx 取消隔行执行 DDI 函数的支持。 \_调用 [**DeinterlaceQueryModeCaps**](./dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)函数时，驱动程序将返回指向 DXVA DeinterlaceCaps 的指针。

显示驱动程序将 DXVA \_ VideoProcess \_ SubStreams 设置为结合取消隔行扫描的视频子流组合。 驱动程序将设置 DXVA \_ VideoProcess \_ STRETCHX 和 DXVA \_ VideoProcess \_ 伸缩，因为视频流和 substreams 的像素纵横比可能不同且不带) ，驱动程序必须能够独立地 (水平和/或垂直为取消隔行扫描提交的视频帧以及提供的视频 substreams。

\_ \_ VideoProcess AlphaBlend 结构的 VideoProcessingCaps 成员中的 DXVA VideoProcess YUV2RGB 和 DXVA \_ DXVA \_ DeinterlaceCaps 标志在驱动程序的 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md)函数的上下文中没有意义。 [**\_**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps) **VideoProcessingCaps** 这些标志与原始 [**DeinterlaceBlt**](./dxva-deinterlacebobdeviceclass-deinterlaceblt.md) 函数相关。 由于支持 *DeinterlaceBltEx* 的显示驱动程序还必须支持 *DeinterlaceBlt*，因此，如果驱动程序在 *DeinterlaceBlt* 的上下文中支持其关联的操作，则该驱动程序仍必须报告这些标志。

### <a name="span-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspanspan-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspanspan-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspandxva_videoprocess_substreamsextended-dxva_videoprocess_yuv2rgbextended-and-dxva_videoprocess_alphablendextended-flags"></a><span id="DXVA_VideoProcess_SubStreamsExtended_DXVA_VideoProcess_YUV2RGBExtended_and_DXVA_VideoProcess_AlphaBlendExtended_flags"></span><span id="dxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flags"></span><span id="DXVA_VIDEOPROCESS_SUBSTREAMSEXTENDED_DXVA_VIDEOPROCESS_YUV2RGBEXTENDED_AND_DXVA_VIDEOPROCESS_ALPHABLENDEXTENDED_FLAGS"></span>DXVA \_ VideoProcess \_ SubStreamsExtended DXVA \_ VIDEOPROCESS \_ YUV2RGBExtended and DXVA \_ VideoProcess \_ AlphaBlendExtended flags

实现 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 函数的显示驱动程序可以为每个源和目标图面支持明显增强的颜色信息。 驱动程序可以通过 \_ \_ \_ \_ \_ \_ 在 [**VideoProcess \_ YUV2RGBExtended**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的 **DXVA** 成员中设置 DXVA VideoProcess SubStreamsExtended、DXVA VideoProcess AlphaBlendExtended 和 VideoProcessingCaps DXVA DeinterlaceCaps 标志来报告此类支持。

支持 DXVA \_ VideoProcess \_ SubStreamsExtended 标志指示显示驱动程序可以对源视频流和 substreams 执行所需的颜色调整。 这些调整会在扩展的颜色数据中指示，因为视频 deinterlaced，与 substreams 复合并写入目标图面。 扩展颜色数据由源示例 (数组的 [**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的 **SampleFormat** 成员中的 [**DXVA \_ ExtendedFormat**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_extendedformat)结构的成员指定，LpDDSrcSurfaces [**\_ DeinterlaceBltEx**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)结构) 的 [**DXVA**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md)调用或 **源** 成员 *中的 DeinterlaceBltEx 参数。*

支持 DXVA \_ VideoProcess \_ YUV2RGBExtended 标记指示显示驱动程序可执行颜色空间转换操作，因为 deinterlaced 和复合像素写入目标图面。 如果将 RGB 目标图面传递到显示器驱动程序，VMR 将确保每个颜色通道至少包含8位。 RGB 目标图面可以是屏幕外、纹理或 Direct3D 呈现器目标，或者是组合纹理和 Direct3D 呈现器目标表面类型。 即使使用了 RGB 目标图面，VMR 仍指定 YUV 颜色空间中的背景色参数。

支持 DXVA \_ VideoProcess \_ AlphaBlendExtended 标志指示在将 deinterlaced 和合成像素写入目标图面时，显示驱动程序可以对目标表面执行 alpha 混合操作。 驱动程序必须根据 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md)调用中 *fAlpha* 参数的 alpha 值处理背景色。 当 alpha 值为 1.0 f 时，背景色会绘制为不透明 (不) 透明。 当 alpha 值为 0.0 f 时，不应 (透明) 绘制背景。

 

