---
title: 支持图形输出
description: 支持图形输出
ms.assetid: 2ac9b01d-9dca-44b4-9645-9c5eefb2ef1b
keywords:
- GDI WDK Windows 2000 显示中，图形输出
- 图形驱动程序 WDK Windows 2000 显示、 输出
- 绘制 WDK GDI，图形输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 814734f90b35c3ccb4a17ae5294af600a22b490c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355537"
---
# <a name="supporting-graphics-output"></a>支持图形输出


## <span id="ddk_supporting_graphics_output_gg"></span><span id="DDK_SUPPORTING_GRAPHICS_OUTPUT_GG"></span>


驱动程序处理特定图形操作取决于绘图图面和硬件的功能。 如果在图面是一种标准格式*DIB*，GDI 将处理所有驱动程序不支持的呈现操作。 该驱动程序可以出任何挂接[的绘图功能](optional-display-driver-functions.md)并实现它们以利用硬件支持。

有关设备管理的面，驱动程序必须至少支持图形输出函数[ **DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)， [ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)并[ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)。 它可以根据需要支持的任何其他图形输出函数。 支持[ **DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)，例如，可以提高性能。 某些功能需要特定级别的功能，而另一些则允许设备通过设置适当的 GCAPS 标志指示其功能[ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构。

所有绘图调用的驱动程序始终是单线程的而不考虑图面上的类型。

后面的主题介绍了如何将驱动程序可以实现以下操作：

[绘制直线和曲线](drawing-lines-and-curves.md)

[绘制并填充路径](drawing-and-filling-paths.md)

[复制位图](copying-bitmaps.md)

[半色调](halftoning.md)

[图像颜色管理](image-color-management.md)

 

 





