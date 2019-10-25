---
title: 提供视频子流和目标图面
description: 提供视频子流和目标图面
ms.assetid: 53528c49-11d1-4e53-b700-f6d8d760bcfe
keywords:
- DeinterlaceBltEx，目标图面
- DeinterlaceBltEx，子流表面
- 目标图面 WDK DirectX VA
- 子流图面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0112f8d13f91488d66d0a7bff383a3f42a74695
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825703"
---
# <a name="supplying-video-substream-and-destination-surfaces"></a>提供视频子流和目标图面


## <span id="ddk_supplying_video_substream_and_destination_surfaces_gg"></span><span id="DDK_SUPPLYING_VIDEO_SUBSTREAM_AND_DESTINATION_SURFACES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 仅为视频 substreams 提供 DXVA 支持的子流表面格式。 也就是说，VMR 仅提供以下*FOURCC*代码用于 alpha 混合子流表面格式： AI44、IA44 或 AYUV。 有关详细信息，请参阅[加载 AYUV Alpha 混合图面](loading-an-ayuv-alpha-blending-surface.md)。 请注意，提供多个视频 substreams 时，每个子流的格式可能不同。 由于所提供视频 substreams 的格式为托盘化 surface 格式，因此，每个图**面的一个**完整的16色调色板都在传递到的数组中的每个[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的调用*DeinterlaceBltEx*时， *pDDSrcSurfaces*参数。 因此，无需驱动程序即可维护每个视频子流图面的调色板信息。

VMR 还只提供格式由驱动程序在[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的**d3dOutputFormat**成员中指定的目标面面。 调用[**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)函数时，驱动程序将返回指向 DXVA\_DeinterlaceCaps 的指针。

 

 





