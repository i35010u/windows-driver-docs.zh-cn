---
title: 处理子矩形
description: 处理子矩形
keywords:
- 取消隔行扫描 WDK DirectX VA，subrectangular 处理
- subrectangular 处理 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b65948bec3720fd8667dcc735fcbf529e70cc9a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838483"
---
# <a name="processing-subrectangles"></a>处理子矩形


## <span id="ddk_processing_subrectangles_gg"></span><span id="DDK_PROCESSING_SUBRECTANGLES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 可以处理源视频图像和视频 substreams 的 subrectangular 区域，并且可以在目标表面上写入 subrectangular 区域。 VMR 执行 subrectangular 操作的方法是：使每个 [**样本的 \_**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2) **rcSrc** 和 **rcDest** 成员中的矩形坐标不同于源和目标曲面的坐标。

如果隔行扫描硬件支持 subrectangular 操作，则显示驱动程序通过 \_ \_ 在 [**VideoProcessingCaps \_ DXVA**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构的 **DeinterlaceCaps** 成员中设置 DXVA VideoProcess SubRects 标志来报告此项支持。 \_调用 [**DeinterlaceQueryModeCaps**](./dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)函数时，驱动程序将返回指向 DXVA DeinterlaceCaps 的指针。

在 subrectangular 操作中，VMR 可以拉伸 subrectangles，并可以在目标图面上交叉 subrectangles。

以下主题说明如何执行各种 subrectangular 操作：

[在不拉伸的情况下处理子矩形](processing-subrectangles-without-stretching.md)

[拉伸子矩形](stretching-subrectangles.md)

 

