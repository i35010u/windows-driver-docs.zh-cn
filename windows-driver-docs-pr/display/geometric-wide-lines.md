---
title: 几何宽线条
description: 几何宽线条
keywords:
- 线条 WDK GDI，几何宽
- GDI WDK Windows 2000 显示、线条、几何宽
- 图形驱动程序 WDK Windows 2000 显示、线条、几何宽
- 绘制 WDK GDI、线条、几何宽
- 几何宽线 WDK GDI
- 几何线条 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e134957ea03521d6816914d50962a3517ac8364
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832411"
---
# <a name="geometric-wide-lines"></a>几何宽线条

*几何* 线条的形状由画笔的宽度、联接样式和端帽样式以及 [**XFORMOBJ**](/previous-versions/windows/hardware/drivers/ff570618(v=vs.85))结构中的当前世界到设备转换决定。 可使用纯色画笔或 nonsolid 画笔绘制线条。

更高级硬件的驱动程序可能支持 [**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath) 函数中的几何宽线。 GDI 确定驱动程序是否可以通过在调用 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)时返回的 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)结构中测试 GCAPS_GEOMETRICWIDE 功能标志来绘制包含几何行的路径。 如果驱动程序没有功能，或者如果该函数因为路径或剪辑对于设备过于复杂而无法处理操作，则 GDI 会自动将调用转换为更简单的 [**DrvFillPath**](/windows/win32/api/winddi/nf-winddi-drvfillpath) 函数。

几何宽线具有显示驱动程序图形函数的特定含义。 如果路径包含设备坐标，则使用当前转换的逆方法转换为世界坐标。 然后，具有指定宽度的几何构造获取更宽的路径版本，并考虑联接和端帽。 此路径再次转换为设备坐标并用指定的画笔填充。

几何宽线的样式由一组浮点值指定。 该数组的长度有限，但使用它，就像它无限重复一样。 第一个数组项指定了第一个短划线的长度（范围为世界坐标）;下一项指定第一个间隙的长度。 此后，将会出现虚线和间隙的长度。 例如，style 数组 {3.0，1.0，1.0，1.0} 会使绘制线条时使用的是长划线和短划线。

可以将样式视为驱动程序在扩展之前在路径上移动，并 "擦除" 路径中对应于间隙的部分。 这会将路径分成多个子路径。 然后，破断路径将被扩大为不具有线条样式，并照常应用端帽和联接。 样式数组的长度可以是奇数。 例如，style 数组 {1.0} 导致驱动程序绘制一条带交替虚线的线条。 样式状态 (定义为到样式数组的当前距离，为路径中第一个子路径的开头提供) 。 它被视为在每个后续子路径开始时重置为0.0，这是在执行任何 Win32 **MoveToEx** 操作之后发生的。
