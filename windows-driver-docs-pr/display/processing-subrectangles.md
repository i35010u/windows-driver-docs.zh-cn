---
title: 处理子矩形
description: 处理子矩形
ms.assetid: d00803c0-98e2-4101-bcfc-ef11fea07962
keywords:
- 取消隔行扫描 WDK DirectX VA，subrectangular 处理
- subrectangular 处理 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3623e9df308fbb75a44a4d1cd2a98d02cae70a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829678"
---
# <a name="processing-subrectangles"></a>处理子矩形


## <span id="ddk_processing_subrectangles_gg"></span><span id="DDK_PROCESSING_SUBRECTANGLES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 可以处理源视频图像和视频 substreams 的 subrectangular 区域，并且可以在目标表面上写入 subrectangular 区域。 VMR 通过将每个样本的**rcSrc**和**rcDest** [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)成员中的矩形坐标作为不同于的坐标，来执行 subrectangular 操作：源和目标面。

如果隔行扫描硬件支持 subrectangular 操作，则显示驱动程序通过在 VideoProcessingCaps 的**DXVA**成员中设置 DXVA\_VideoProcess\_SubRects 标志来报告此支持[ **\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)结构。 调用[**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)函数时，驱动程序将返回指向 DXVA\_DeinterlaceCaps 的指针。

在 subrectangular 操作中，VMR 可以拉伸 subrectangles，并可以在目标图面上交叉 subrectangles。

以下主题说明如何执行各种 subrectangular 操作：

[不拉伸处理 Subrectangles](processing-subrectangles-without-stretching.md)

[拉伸 Subrectangles](stretching-subrectangles.md)

 

 





