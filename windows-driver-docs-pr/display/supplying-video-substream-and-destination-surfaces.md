---
title: 提供视频子流和目标图面
description: 提供视频子流和目标图面
ms.assetid: 53528c49-11d1-4e53-b700-f6d8d760bcfe
keywords:
- DeinterlaceBltEx，目标图面
- DeinterlaceBltEx，子流图面
- 目标的图面 WDK DirectX VA
- 子流图面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9acc2fe84ac85ee53f80cd9f2dd4754257be911
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375913"
---
# <a name="supplying-video-substream-and-destination-surfaces"></a>提供视频子流和目标图面


## <span id="ddk_supplying_video_substream_and_destination_surfaces_gg"></span><span id="DDK_SUPPLYING_VIDEO_SUBSTREAM_AND_DESTINATION_SURFACES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

VMR Windows Server 2003 SP1 及更高版本和 Windows XP SP2 和更高版本仅提供视频子流与子流图面 DXVA 支持的格式。 也就是说，VMR 只会提供以下*FOURCC* alpha 值混合处理子流图面格式的代码：AI44、 IA44 或 AYUV。 有关详细信息，请参阅[加载 AYUV Alpha 值混合处理的图面](loading-an-ayuv-alpha-blending-surface.md)。 请注意，如果提供多个视频的子流，每个子流可能会进行不同的格式。 由于提供的视频子流的格式是图面上的托盘化的格式，因此中提供完成每个面的 16 色调色板**调色板**的每个成员[ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)中的数组中传递的结构*pDDSrcSurfaces*参数时*DeinterlaceBltEx*调用。 因此，该驱动程序不需要维护每个视频的子流图面调色板信息。

VMR 也只会提供其格式中的驱动程序通过将指定的目标表面**d3dOutputFormat**的成员[ **DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)结构。 该驱动程序返回一个指向 DXVA\_DeinterlaceCaps 时其[ **DeinterlaceQueryModeCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563946)调用函数。

 

 





