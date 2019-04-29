---
title: 几何宽线条
description: 几何宽线条
ms.assetid: 769b801c-6950-4f0f-9163-c4ddf070e519
keywords:
- 行 WDK GDI，几何范围
- GDI WDK Windows 2000 显示、 线、 几何范围
- 图形驱动程序 WDK Windows 2000 显示，行，几何范围
- 绘制 WDK GDI，行，几何范围
- 几何宽线条 WDK GDI
- 几何行 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f5107e6d12480f11309c8c39e7974099755edb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373451"
---
# <a name="geometric-wide-lines"></a>几何宽线条


## <span id="ddk_geometric_wide_lines_gg"></span><span id="DDK_GEOMETRIC_WIDE_LINES_GG"></span>


形状*几何*行由宽度、 联接样式和画笔和中的当前到设备的世界转换的结束帽样式[ **XFORMOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570618)结构。 可以使用纯色或非实体的画笔绘制线条。

更高级的硬件驱动程序可能支持在几何宽线条[ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)函数。 GDI 确定驱动程序是否可以绘制路径几何行包含通过测试 GCAPS\_GEOMETRICWIDE 中的功能标志[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835) 调用中返回的结构[**DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)。 如果该驱动程序不具有功能，或者如果函数失败以处理操作，因为路径或剪辑太过复杂，该设备，GDI 自动转换到更简单的调用[ **DrvFillPath**](https://msdn.microsoft.com/library/windows/hardware/ff556220)函数。

几何宽行具有显示驱动程序图形函数到特定的含义。 包含设备坐标的路径转换为使用当前变换的逆变换世界坐标。 使用指定的宽度的几何构造然后获取路径，考虑到帐户联接和末端的加宽的版本。 此路径是再次转换为设备坐标，用指定画笔填充。

几何加宽线的样式设置被指定的浮点值的数组。 数组长度有限，但是，就好像它无限期地重复使用。 第一个数组项的第一个破折号; 的世界坐标中指定的长度下一个条目指定的第一个间隙的长度。 在此之后，备用短划线和间隙的长度。 例如，样式数组 {3.0,1.0,1.0,1.0} 会导致要使用交替长、 短划线绘制的行。

样式可以看作扩大转换，先沿着路径移动的驱动程序"擦除"对应于间隙的路径组成部分。 这将分成多个子路径的路径。 然后它扩展中断的路径，因为如果它没有线条样式，像往常一样将结束端点和连接的应用。 奇数长度可以是样式数组。 例如，样式数组中 {1.0} 会导致要绘制一个行，其中交替短划线的驱动程序。 样式状态 （定义为样式数组中的当前距离） 提供的路径中的第一个子路径的起始位置。 它将被视为重置为 0.0 的任何 Win32 之后发生每个后续子路径开头**MoveToEx**操作。

 

 





