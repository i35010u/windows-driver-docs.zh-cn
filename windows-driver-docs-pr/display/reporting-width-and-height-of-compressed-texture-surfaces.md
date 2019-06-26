---
title: 报告压缩纹理图面的宽度和高度
description: 报告压缩纹理图面的宽度和高度
ms.assetid: 262262b6-9fef-4f28-beec-373f78a10f8f
keywords:
- WDK DirectDraw，压缩的纹理的图面
- 纹理 WDK DirectDraw 压缩
- 绘制压缩纹理 WDK DirectDraw，宽度
- DirectDraw 显示压缩的纹理 WDK Windows 2000 宽度
- 压缩的纹理图面 WDK DirectDraw，宽度
- 绘制压缩纹理 WDK DirectDraw，高度
- DirectDraw 显示压缩的纹理 WDK Windows 2000 高度
- 压缩的纹理图面 WDK DirectDraw，高度
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1236314e7cf2aab592f7deb7903dc5bd6effb23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375907"
---
# <a name="reporting-width-and-height-of-compressed-texture-surfaces"></a>报告压缩纹理图面的宽度和高度


## <span id="ddk_reporting_width_and_height_of_compressed_texture_surfaces_gg"></span><span id="DDK_REPORTING_WIDTH_AND_HEIGHT_OF_COMPRESSED_TEXTURE_SURFACES_GG"></span>


DirectX 运行时请求驱动程序创建 DXT*n*压缩的纹理图面上其宽度和高度都小于 4 × 4，驱动程序实际分配 4x4 块的内存为纹理图面。 但是，该驱动程序报告的宽度和高度的纹理图面作为运行时请求的值。 例如，如果请求 2 x 2 DXT1 压缩的纹理图面，则驱动程序分配 4x4 块，但报告的块通过保持不变的请求的纹理大小是 2x2。 若要请求特定 DXT*n*压缩纹理大小，运行时集**dwWidth**并**dwHeight**的成员[ **DDSURFACEDESC** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550339(v=vs.85))或[ **DDSURFACEDESC2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构，它表示纹理图面。 该驱动程序不会更改这些大小设置，即使它会分配 4 × 4 纹理图面，该请求是针对其宽度和高度都小于 4 × 4 纹理图面。

 

 





