---
title: 报告压缩纹理图面的宽度和高度
description: 报告压缩纹理图面的宽度和高度
ms.assetid: 262262b6-9fef-4f28-beec-373f78a10f8f
keywords:
- 表面 WDK DirectDraw，压缩纹理
- 纹理 WDK DirectDraw，压缩
- 绘制压缩纹理 WDK DirectDraw，width
- DirectDraw 压缩纹理 WDK Windows 2000 显示，宽度
- 压缩的纹理面 WDK DirectDraw，width
- 绘制压缩纹理 WDK DirectDraw，高度
- DirectDraw 压缩纹理 WDK Windows 2000 显示，高度
- 压缩的纹理面 WDK DirectDraw，高度
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc304f913077613189c9c4186fedbe04ebfbf65c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067240"
---
# <a name="reporting-width-and-height-of-compressed-texture-surfaces"></a>报告压缩纹理图面的宽度和高度


## <span id="ddk_reporting_width_and_height_of_compressed_texture_surfaces_gg"></span><span id="DDK_REPORTING_WIDTH_AND_HEIGHT_OF_COMPRESSED_TEXTURE_SURFACES_GG"></span>


当 DirectX 运行时请求驱动程序创建一个宽度和高度小于4x4 的 DXT*n* 压缩纹理图面时，驱动程序会实际为纹理图面分配一个4x4 内存块。 但是，驱动程序会报告纹理图面的宽度和高度，作为运行时请求的值。 例如，如果请求 2x2 DXT1 压缩纹理图面，则驱动程序将分配一个4x4 块，但会通过保持请求的纹理大小不变来报告块为2x2。 若要请求特定的*DXT n*压缩纹理大小，运行时将设置表示纹理图面的[**DDSURFACEDESC**](/previous-versions/windows/hardware/drivers/ff550339(v=vs.85))或[**DDSURFACEDESC2**](/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构的**dwWidth**和**dwHeight**成员。 即使请求适用于宽度和高度小于4x4 的纹理图面，驱动程序也不会更改这些大小设置。

 

