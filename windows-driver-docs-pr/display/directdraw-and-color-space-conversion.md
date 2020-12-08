---
title: DirectDraw 和色彩空间转换
description: DirectDraw 和色彩空间转换
keywords:
- surface DirectDraw，blitting
- 绘制 blt WDK DirectDraw，颜色空间转换
- DirectDraw blitting WDK Windows 2000 显示，颜色空间转换
- blitting WDK DirectDraw，颜色空间转换
- blt WDK DirectDraw，颜色空间转换
- YUV 格式 WDK DirectDraw
- Fourcc
- 颜色空间 WDK DirectDraw
- 转换颜色空间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0aa0e215c59c1ebeff6e26f7c4df36d14f12c4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809413"
---
# <a name="directdraw-and-color-space-conversion"></a>DirectDraw 和色彩空间转换


## <span id="ddk_directdraw_and_color_space_conversion_gg"></span><span id="DDK_DIRECTDRAW_AND_COLOR_SPACE_CONVERSION_GG"></span>


DirectDraw 允许以 YUV 格式创建和存储图面。 四个字符代码 (*fourcc*) 指示正在使用的颜色空间转换。 然后，在覆盖过程中，将图像转换为16位 RGB。 YUV 4:2:2 的密度与每个像素 (bpp) 的16位有效，但颜色保真度更好。 可以将该图像作为 YUV 写入，并以 RGB 形式进入显示内存，但通常会在显示内存时进行转换，以便保留压缩。 这会保存显示内存并加速播放。 对于 Windows 2000 及更高版本，某些 YUV 格式 (UYVY 和 YUY2 ˆ），这两种类型的 4:2:2) 均被模拟，但仅当用作纹理时才可使用。 请注意，不支持在系统内存中创建不支持的 YUV 格式的图面。

以下三个常见的 YUV 颜色空间为：

-   4:2:2 (标准电视属于此类型) 

-   4:1:1 (更多压缩) 

-   4:4:4 (类似于 RGB) 

目前使用的是这些颜色空间和许多其他的 YUV 格式。 有关 FOURCC 的信息，请参阅 [FOURCC](https://go.microsoft.com/fwlink/p/?linkid=8697) 网站。

 

 





