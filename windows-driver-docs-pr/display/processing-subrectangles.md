---
title: 处理子矩形
description: 处理子矩形
ms.assetid: d00803c0-98e2-4101-bcfc-ef11fea07962
keywords:
- 取消隔行扫描 WDK DirectX VA，subrectangular 处理
- subrectangular 处理 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e50070bbba1ad2303dde2eedf6b84dbd5ddf428
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363704"
---
# <a name="processing-subrectangles"></a>处理子矩形


## <span id="ddk_processing_subrectangles_gg"></span><span id="DDK_PROCESSING_SUBRECTANGLES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

在 Windows Server 2003 SP1 及更高版本的 VMR 和 Windows XP SP2 和更高版本可以处理的源视频图像和视频的子流 subrectangular 区域，并可以写入到 subrectangular 区域目标图面上。 VMR 执行 subrectangular 处理操作，从而在矩形的坐标**rcSrc**并**rcDest**的成员[ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)结构不同的源和目标的图面坐标从每个示例。

如果取消隔行扫描硬件支持 subrectangular 处理操作，显示器驱动程序将报告这种支持通过设置 DXVA\_VideoProcess\_SubRects 标志中**VideoProcessingCaps**成员[ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)结构。 该驱动程序返回一个指向 DXVA\_DeinterlaceCaps 时其[ **DeinterlaceQueryModeCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)调用函数。

Subrectangular 处理操作中 VMR subrectangles 就能够拉伸和可以 intersect subrectangles 与每个其他目标图面上。

以下主题演示如何执行各种 subrectangular 过程操作：

[处理 Subrectangles 而不是拉伸](processing-subrectangles-without-stretching.md)

[拉伸 Subrectangles](stretching-subrectangles.md)

 

 





