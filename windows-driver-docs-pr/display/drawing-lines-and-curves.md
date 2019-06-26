---
title: 绘制线条和曲线
description: 绘制线条和曲线
ms.assetid: 0816fb69-7811-4319-b050-00ded21a10d4
keywords:
- 行 WDK GDI
- GDI WDK Windows 2000 显示中行
- 图形驱动程序 WDK Windows 2000 显示行
- 绘制 WDK GDI，行
- GDI WDK Windows 2000 显示曲线
- 图形驱动程序 WDK Windows 2000 显示曲线
- 绘制 WDK GDI，曲线
- 画笔 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e754ff086b91da9acbbb97fecf29e30687e998a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365729"
---
# <a name="drawing-lines-and-curves"></a>绘制线条和曲线


## <span id="ddk_drawing_lines_and_curves_gg"></span><span id="DDK_DRAWING_LINES_AND_CURVES_GG"></span>


直线和曲线图形输出中包含的类型为[几何行](geometric-wide-lines.md)，[修饰的行](cosmetic-lines.md)，并[贝塞尔曲线](bezier-curves.md)。

驱动程序支持的直线和曲线输出[ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)， [ **DrvFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)，和[ **DrvStrokeAndFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)函数。 该驱动程序必须支持**DrvStrokePath**用于绘制线条，如果在图面是设备管理; 驱动程序不需要支持曲线。

在 GDI 绘制线条或曲线，任何一组属性，可以调用 GDI [ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)。 最低限度**DrvStrokePath**函数必须支持使用纯色画笔 solid 和带样式修饰线的绘图和任意剪辑。 GDI PATHOBJ\_*Xxx*和 CLIPOBJ\_*Xxx*服务功能做到这一点通过将分解成一组行一个像素宽与预计算剪辑的行。 **DrvStrokePath**提供一个指针**plineattrs**到[ **LINEATTRS** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_lineattrs)结构，它定义不同的线条特性。

过于复杂，驱动程序来处理在设备上的路径或剪切时，该驱动程序可以稍作回调到 GDI 通过调用[ **EngStrokePath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engstrokepath)函数。 在这种情况下，可能会中断 GDI [ **DrvStrokePath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)调入一组行一个像素宽与预计算的剪辑。

通过调用 CLIPOBJ\_*Xxx*从 GDI 的服务，驱动程序可以具有 GDI 枚举路径中的所有行并执行所有的行剪辑计算。 此外，驱动程序可以使用 PATHOBJ\_*Xxx*，CLIPOBJ\_*Xxx*，或 XFORMOBJ\_*Xxx*服务来简化图形操作。 例如，可以使用驱动程序**CLIPOBJ\_cEnumStart**、 发送到打印机，此区域和剪裁到它。 此外可以使用该驱动程序[ **PATHOBJ\_vEnumStart** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_venumstart)并[ **PATHOBJ\_bEnum** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-pathobj_benum)枚举行或在路径中的曲线。 然后可以将路径发送到设备，并绘制它。

 

 





