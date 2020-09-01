---
title: 绘制和填充路径
description: 绘制和填充路径
ms.assetid: bc31aeba-d1f1-4e38-a8df-19e8d7e178c7
keywords:
- GDI WDK Windows 2000 显示，路径
- 图形驱动程序 WDK Windows 2000 显示，路径
- 绘制 WDK GDI，路径
- 填充路径 WDK GDI
- 路径 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c596e54aec11f55f48c122d128f77c01059ddf6b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065482"
---
# <a name="drawing-and-filling-paths"></a>绘制和填充路径


## <span id="ddk_drawing_and_filling_paths_gg"></span><span id="DDK_DRAWING_AND_FILLING_PATHS_GG"></span>


图形驱动程序将路径视为由路径对象定义的一系列线条和/或曲线 ([**PATHOBJ**](/windows/desktop/api/winddi/ns-winddi-_pathobj) 结构) 。 为了处理已关闭的路径，驱动程序支持函数 [**DrvFillPath**](/windows/desktop/api/winddi/nf-winddi-drvfillpath)。

GDI 可以调用 [**DrvFillPath**](/windows/desktop/api/winddi/nf-winddi-drvfillpath) 来填充设备管理的图面上的路径。 GDI 将填充要求与 [**lnk-devinfo**](/windows/desktop/api/winddi/ns-winddi-tagdevinfo) 结构的标志 GCAPS \_ 贝塞尔、GCAPS \_ ALTERNATEFILL 和 GCAPS WINDINGFILL 进行比较 \_ ，以决定是否调用驱动程序。 如果 GDI 调用了驱动程序，则驱动程序将执行操作或返回，通知 GDI：请求的路径或剪辑太复杂，无法由设备处理。 在后一种情况下，GDI 会将请求分解为几个简单的操作。

驱动程序还可以支持可选的 [**DrvStrokeAndFillPath**](/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath) 函数，以满足对路径填充的请求。 此函数同时填充和笔划路径。 许多 GDI 基元都需要此功能。 如果将宽线用于描边，则必须减小填充区域，以弥补边界路径增加的宽度。

当驱动程序从[**DrvFillPath**](/windows/desktop/api/winddi/nf-winddi-drvfillpath)或[**DrvStrokeAndFillPath**](/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)函数返回**FALSE**时，GDI 会将填充路径请求转换为一组更简单的操作并再次调用驱动程序函数。 如果在第二次调用**DrvFillPath**时设备再次返回**FALSE** ，则 GDI 将路径转换为剪辑对象，然后调用[**EngFillPath**](/windows/desktop/api/winddi/nf-winddi-engfillpath)。 对于**DrvStrokeAndFillPath**回调时的**FALSE**返回，GDI 可以将调用转换为单独调用[**DrvStrokePath**](/windows/desktop/api/winddi/nf-winddi-drvstrokepath)和**DrvFillPath**。

 

