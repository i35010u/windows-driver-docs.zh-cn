---
title: 绘制和填充路径
description: 绘制和填充路径
ms.assetid: bc31aeba-d1f1-4e38-a8df-19e8d7e178c7
keywords:
- GDI WDK Windows 2000 显示中路径
- 图形驱动程序 WDK Windows 2000 显示路径
- 绘制 WDK GDI，路径
- 填充路径 WDK GDI
- 路径 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ec62cd3663ca2c3fe534d62eac8daa2aba75bd3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365727"
---
# <a name="drawing-and-filling-paths"></a>绘制和填充路径


## <span id="ddk_drawing_and_filling_paths_gg"></span><span id="DDK_DRAWING_AND_FILLING_PATHS_GG"></span>


图形驱动程序会考虑要为一系列行，和/或曲线，由一个路径对象定义的路径 ([**PATHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)结构)。 若要处理的已关闭的路径的填充，该驱动程序支持的函数[ **DrvFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)。

可以调用 GDI [ **DrvFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)以填充设备管理的图面上的路径。 GDI 进行比较的要求与填充[ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构的标志 GCAPS\_贝赛尔曲线、 GCAPS\_ALTERNATEFILL 和 GCAPS\_WINDINGFILL 到决定是否调用该驱动程序。 如果 GDI does 调用驱动程序，该驱动程序则将执行的操作或返回时，通知 GDI 中的路径或剪辑请求太过复杂，要由该设备。 在后一种情况下，GDI 细分请求为多个更简单的操作。

驱动程序还支持可选[ **DrvStrokeAndFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)函数来满足请求的路径填充。 此函数填充，并在同一时间描边的路径。 许多 GDI 原型需要此功能。 如果宽行用于描画，必须降低填充的区域来弥补增加宽度的边框的路径。

当驱动程序将返回**FALSE**眖[ **DrvFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)或者[ **DrvStrokeAndFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)函数，GDI 将填充路径请求转换为一组更简单的操作和会再次调用驱动程序函数。 如果设备返回**FALSE**再次在第二个调用**DrvFillPath**，GDI 将路径转换为剪辑对象，然后调用[ **EngFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath). 有关**FALSE**返回时**DrvStrokeAndFillPath** GDI 可以将调用转换成单独调用的召回[ **DrvStrokePath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)并**DrvFillPath**。

 

 





