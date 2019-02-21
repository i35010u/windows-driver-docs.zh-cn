---
title: 报告对 DeinterlaceBltEx 的支持
description: 报告对 DeinterlaceBltEx 的支持
ms.assetid: 9cf8d05c-ef59-44a4-a377-66282e7888d5
keywords:
- DeinterlaceBltEx，报告
- DXVA_VideoProcess_SubStreamsExtended
- DXVA_VideoProcess_YUV2RGBExtended
- DXVA_VideoProcess_AlphaBlendExtended
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6081399bb60914df9e97e41fe4405121f9d44bb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523825"
---
# <a name="reporting-support-for-deinterlacebltex"></a>报告对 DeinterlaceBltEx 的支持


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

显示驱动程序报告的支持[ **DeinterlaceBltEx**](https://msdn.microsoft.com/library/windows/hardware/ff563927)[取消隔行扫描 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552701)函数通过设置 DXVA\_VideoProcess\_子流、 DXVA\_VideoProcess\_StretchX 和 DXVA\_VideoProcess\_StretchY 标志中**VideoProcessingCaps**隶属[**DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)结构。 该驱动程序返回一个指向 DXVA\_DeinterlaceCaps 时其[ **DeinterlaceQueryModeCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563946)调用函数。

显示驱动程序设置 DXVA\_VideoProcess\_子流合并视频的子流与去隔行组合的情况。 驱动程序设置 DXVA\_VideoProcess\_StretchX 和 DXVA\_VideoProcess\_因为像素纵横比的视频流和子流可以是不同的域和非方形，并且该驱动程序必须能够伸缩为独立延伸 （水平和/或垂直） 视频帧的提交进行去隔行以及提供视频子流。

DXVA\_VideoProcess\_YUV2RGB 和 DXVA\_VideoProcess\_AlphaBlend 标志中**VideoProcessingCaps**隶属[ **DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)结构的驱动程序的上下文中没有任何意义[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)函数。 这些标志与原始[ **DeinterlaceBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff563924)函数。 由于显示器驱动程序的支持，因此*DeinterlaceBltEx*还必须支持*DeinterlaceBlt*，驱动程序必须仍会报告这些标志，如果它支持上下文中其关联的操作*DeinterlaceBlt*。

### <a name="span-iddxvavideoprocesssubstreamsextendeddxvavideoprocessyuv2rgbextendedanddxvavideoprocessalphablendextendedflagsspanspan-iddxvavideoprocesssubstreamsextendeddxvavideoprocessyuv2rgbextendedanddxvavideoprocessalphablendextendedflagsspanspan-iddxvavideoprocesssubstreamsextendeddxvavideoprocessyuv2rgbextendedanddxvavideoprocessalphablendextendedflagsspandxvavideoprocesssubstreamsextended-dxvavideoprocessyuv2rgbextended-and-dxvavideoprocessalphablendextended-flags"></a><span id="DXVA_VideoProcess_SubStreamsExtended_DXVA_VideoProcess_YUV2RGBExtended_and_DXVA_VideoProcess_AlphaBlendExtended_flags"></span><span id="dxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flags"></span><span id="DXVA_VIDEOPROCESS_SUBSTREAMSEXTENDED_DXVA_VIDEOPROCESS_YUV2RGBEXTENDED_AND_DXVA_VIDEOPROCESS_ALPHABLENDEXTENDED_FLAGS"></span>DXVA\_VideoProcess\_SubStreamsExtended DXVA\_VideoProcess\_YUV2RGBExtended 和 DXVA\_VideoProcess\_AlphaBlendExtended 标志

显示驱动程序实现[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)函数可为每个源和目标的图面提供支持极大的增强的颜色信息。 该驱动程序可以报告此类支持通过设置 DXVA\_VideoProcess\_SubStreamsExtended、 DXVA\_VideoProcess\_YUV2RGBExtended 和 DXVA\_VideoProcess\_在标记 AlphaBlendExtended **VideoProcessingCaps**的成员[ **DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)结构。

支持 DXVA\_VideoProcess\_SubStreamsExtended 标志指示显示器驱动程序，可以执行的源视频流和子流的必要颜色调整。 这些调整会指示扩展的颜色数据中，如视频是 deinterlaced、 表面与子流，并写入到目标图面。 扩展的颜色数据指定的成员[ **DXVA\_ExtendedFormat** ](https://msdn.microsoft.com/library/windows/hardware/ff563967)结构**SampleFormat**成员[ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)结构的源示例数组 (*lpDDSrcSurfaces*中的参数[ **DeinterlaceBltEx**](https://msdn.microsoft.com/library/windows/hardware/ff563927)调用或**源**的成员[ **DXVA\_DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563915)结构)。

支持 DXVA\_VideoProcess\_YUV2RGBExtended 标志指示 deinterlaced 和复合像素写入到目标图面，显示器驱动程序，可以执行的颜色空间转换运算。 如果 RGB 目标面传递给显示器驱动程序，可确保 VMR，每个颜色通道包含至少为 8 位。 RGB 目标面可能是屏幕外，纹理或 Direct3D 呈现器目标，或组合的纹理和 Direct3D 呈现目标图面类型。 VMR 仍指定背景颜色参数中的 YUV 颜色空间即使使用 RGB 目标图面。

支持 DXVA\_VideoProcess\_AlphaBlendExtended 标志指示 deinterlaced 和复合像素为单位写入时，显示器驱动程序，可以执行与目标面 alpha 混合操作目标面。 该驱动程序必须处理 alpha 值的基础的背景色*fAlpha*中的参数[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)调用。 1.0f alpha 值时，背景色绘制不透明 （而不透明度）。 0.0f 的 alpha 值时，应不绘制背景 （透明）。

 

 





