---
title: 绘制并填充路径
description: 绘制并填充路径
ms.assetid: bc31aeba-d1f1-4e38-a8df-19e8d7e178c7
keywords:
- GDI WDK Windows 2000 显示中路径
- 图形驱动程序 WDK Windows 2000 显示路径
- 绘制 WDK GDI，路径
- 填充路径 WDK GDI
- 路径 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e6fbe39ea55055b243bdc6befb934fb2a44435a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534373"
---
# <a name="drawing-and-filling-paths"></a>绘制并填充路径


## <span id="ddk_drawing_and_filling_paths_gg"></span><span id="DDK_DRAWING_AND_FILLING_PATHS_GG"></span>


图形驱动程序会考虑要为一系列行，和/或曲线，由一个路径对象定义的路径 ([**PATHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff568849)结构)。 若要处理的已关闭的路径的填充，该驱动程序支持的函数[ **DrvFillPath**](https://msdn.microsoft.com/library/windows/hardware/ff556220)。

可以调用 GDI [ **DrvFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff556220)以填充设备管理的图面上的路径。 GDI 进行比较的要求与填充[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构的标志 GCAPS\_贝赛尔曲线、 GCAPS\_ALTERNATEFILL 和 GCAPS\_WINDINGFILL 到决定是否调用该驱动程序。 如果 GDI does 调用驱动程序，该驱动程序则将执行的操作或返回时，通知 GDI 中的路径或剪辑请求太过复杂，要由该设备。 在后一种情况下，GDI 细分请求为多个更简单的操作。

驱动程序还支持可选[ **DrvStrokeAndFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff556311)函数来满足请求的路径填充。 此函数填充，并在同一时间描边的路径。 许多 GDI 原型需要此功能。 如果宽行用于描画，必须降低填充的区域来弥补增加宽度的边框的路径。

当驱动程序将返回**FALSE**眖[ **DrvFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff556220)或者[ **DrvStrokeAndFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff556311)函数，GDI 将填充路径请求转换为一组更简单的操作和会再次调用驱动程序函数。 如果设备返回**FALSE**再次在第二个调用**DrvFillPath**，GDI 将路径转换为剪辑对象，然后调用[ **EngFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff564860). 有关**FALSE**返回时**DrvStrokeAndFillPath** GDI 可以将调用转换成单独调用的召回[ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)并**DrvFillPath**。

 

 





