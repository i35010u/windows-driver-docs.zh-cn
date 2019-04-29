---
title: DirectDraw 和色彩空间转换
description: DirectDraw 和色彩空间转换
ms.assetid: 2a5e59ea-2190-4701-ab7b-7a6503aec6e5
keywords:
- WDK DirectDraw 图阵的图面
- 绘制 blt WDK DirectDraw，颜色空间转换
- DirectDraw 图阵 WDK Windows 2000 显示，颜色空间转换
- 平面闪 WDK DirectDraw，颜色空间转换
- blt WDK DirectDraw，颜色空间转换
- YUV 格式 WDK DirectDraw
- Fourcc
- 颜色空间 WDK DirectDraw
- 将颜色空间转换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c69d786d137f5f7e0559539afa9e31c9ff581e77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358259"
---
# <a name="directdraw-and-color-space-conversion"></a>DirectDraw 和色彩空间转换


## <span id="ddk_directdraw_and_color_space_conversion_gg"></span><span id="DDK_DIRECTDRAW_AND_COLOR_SPACE_CONVERSION_GG"></span>


DirectDraw 允许图面以创建并存储在 YUV 格式。 四字符代码 (*Fourcc*) 表示正在使用何种颜色空间转换。 然后，在覆盖过程中，图像转换为 16 位 RGB。 YUV 4:2:2 实际上是相同的密度，以每像素 (bpp)，16 位，但最好还是色彩保真度。 映像可以编写为 YUV，并转到将内存显示为 RGB，但通常情况下进行转换，以便维护压缩读取显示内存不足。 这会保存显示内存并提高播放速度。 Windows 2000 和更高版本，某些 YUV 格式 (UYVY 和 YUY2 âˆ 4 这两种类型： 2:2) 仿真，但只有当用作纹理时。 请注意，不能在系统内存中创建不受支持的 YUV 格式图面。

三个常用的 YUV 颜色空间是：

-   4:2:2 （为此类型的标准电视）

-   4:1:1 （更压缩）

-   4:4:4 （类似于 RGB）

目前，许多类型的这些颜色空间和使用中的许多其他 YUV 格式。 FOURCC 有关的信息，请转到[FOURCC](https://go.microsoft.com/fwlink/p/?linkid=8697)网站。

 

 





