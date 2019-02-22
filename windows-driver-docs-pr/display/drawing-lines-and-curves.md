---
title: 绘制直线和曲线
description: 绘制直线和曲线
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
ms.openlocfilehash: 085512c36bfec63b9fa0eb16fab025108d42f1d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545961"
---
# <a name="drawing-lines-and-curves"></a>绘制直线和曲线


## <span id="ddk_drawing_lines_and_curves_gg"></span><span id="DDK_DRAWING_LINES_AND_CURVES_GG"></span>


直线和曲线图形输出中包含的类型为[几何行](geometric-wide-lines.md)，[修饰的行](cosmetic-lines.md)，并[贝塞尔曲线](bezier-curves.md)。

驱动程序支持的直线和曲线输出[ **DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)， [ **DrvFillPath**](https://msdn.microsoft.com/library/windows/hardware/ff556220)，和[ **DrvStrokeAndFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff556311)函数。 该驱动程序必须支持**DrvStrokePath**用于绘制线条，如果在图面是设备管理; 驱动程序不需要支持曲线。

在 GDI 绘制线条或曲线，任何一组属性，可以调用 GDI [ **DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)。 最低限度**DrvStrokePath**函数必须支持使用纯色画笔 solid 和带样式修饰线的绘图和任意剪辑。 GDI PATHOBJ\_*Xxx*和 CLIPOBJ\_*Xxx*服务功能做到这一点通过将分解成一组行一个像素宽与预计算剪辑的行。 **DrvStrokePath**提供一个指针**plineattrs**到[ **LINEATTRS** ](https://msdn.microsoft.com/library/windows/hardware/ff568195)结构，它定义不同的线条特性。

过于复杂，驱动程序来处理在设备上的路径或剪切时，该驱动程序可以稍作回调到 GDI 通过调用[ **EngStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff565033)函数。 在这种情况下，可能会中断 GDI [ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)调入一组行一个像素宽与预计算的剪辑。

通过调用 CLIPOBJ\_*Xxx*从 GDI 的服务，驱动程序可以具有 GDI 枚举路径中的所有行并执行所有的行剪辑计算。 此外，驱动程序可以使用 PATHOBJ\_*Xxx*，CLIPOBJ\_*Xxx*，或 XFORMOBJ\_*Xxx*服务来简化图形操作。 例如，可以使用驱动程序**CLIPOBJ\_cEnumStart**、 发送到打印机，此区域和剪裁到它。 此外可以使用该驱动程序[ **PATHOBJ\_vEnumStart** ](https://msdn.microsoft.com/library/windows/hardware/ff568856)并[ **PATHOBJ\_bEnum** ](https://msdn.microsoft.com/library/windows/hardware/ff568851)枚举行或在路径中的曲线。 然后可以将路径发送到设备，并绘制它。

 

 





