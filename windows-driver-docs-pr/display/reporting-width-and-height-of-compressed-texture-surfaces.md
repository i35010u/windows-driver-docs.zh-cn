---
title: 报告压缩纹理图面的宽度和高度
description: 报告压缩纹理图面的宽度和高度
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
ms.openlocfilehash: 498747f7fc76cec70e376f6381d897a11fc202d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840177"
---
# <a name="reporting-width-and-height-of-compressed-texture-surfaces"></a>报告压缩纹理图面的宽度和高度


## <span id="ddk_reporting_width_and_height_of_compressed_texture_surfaces_gg"></span><span id="DDK_REPORTING_WIDTH_AND_HEIGHT_OF_COMPRESSED_TEXTURE_SURFACES_GG"></span>


当 DirectX 运行时请求驱动程序创建一个宽度和高度小于4x4 的 DXT *n* 压缩纹理图面时，驱动程序会实际为纹理图面分配一个4x4 内存块。 但是，驱动程序会报告纹理图面的宽度和高度，作为运行时请求的值。 例如，如果请求 2x2 DXT1 压缩纹理图面，则驱动程序将分配一个4x4 块，但会通过保持请求的纹理大小不变来报告块为2x2。 若要请求特定的 *DXT n* 压缩纹理大小，运行时将设置表示纹理图面的 [**DDSURFACEDESC**](/previous-versions/windows/hardware/drivers/ff550339(v=vs.85))或 [**DDSURFACEDESC2**](/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构的 **dwWidth** 和 **dwHeight** 成员。 即使请求适用于宽度和高度小于4x4 的纹理图面，驱动程序也不会更改这些大小设置。

 

