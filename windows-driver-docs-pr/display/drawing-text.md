---
title: 绘制文本
description: 绘制文本
ms.assetid: e5bf4673-93c4-4cc5-b74d-e0e3a487ec3d
keywords:
- GDI WDK Windows 2000 显示、 文本输出
- 图形驱动程序 WDK Windows 2000 显示、 文本输出
- 文本输出 WDK 图形
- DrvTextOut
- DrvGetGlyphMode
- 图面上的文本输出 WDK GDI
- GDI WDK Windows 2000 显示、 文本输出，绘制
- 显示图形驱动程序 WDK Windows 2000，绘制的文本输出
- WDK GDI 绘制文本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac8d72b24cbda278234b7520b8aefac9f9d04807
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377679"
---
# <a name="drawing-text"></a>绘制文本


## <span id="ddk_drawing_text_gg"></span><span id="DDK_DRAWING_TEXT_GG"></span>


文本输出函数调用仅对*设备管理面*（设备位图或图面），或如果该驱动程序已挂钩中的调用 GDI 托管面的[ **EngAssociateSurface**](https://msdn.microsoft.com/library/windows/hardware/ff564183)函数。 文本的图形输出基元是的功能：

[**DrvTextOut**](https://msdn.microsoft.com/library/windows/hardware/ff557277)

[**DrvGetGlyphMode**](https://msdn.microsoft.com/library/windows/hardware/ff556230)

GDI 调用**DrvTextOut**来呈现标志符号的文本输出指定位置处的一组像素。 许多**DrvTextOut**功能定义与 GCAPS 位[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)返回的结构[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)函数。

输入的参数的**DrvTextOut**定义两个集的像素为单位*前台*并*不透明*。 该驱动程序将呈现图面提供了以下结果：

1.  首先，使用不透明画笔呈现不透明的像素为单位。

2.  然后使用前景画笔呈现前台像素。

在中执行的每个这些呈现操作*剪辑区域*。 不能受影响的剪辑区域外部的像素。

驱动程序必须呈现图面，使计算，图面上首先绘制不透明画笔的不透明的像素为单位。 然后前台像素为单位计算和呈现的前景画笔。 这些操作受到剪辑。

前景色和不透明像素构成了一个掩码，通过该颜色碰在图面。 一种字体的标志符号，本身，没有颜色。 像素的前景色集定义为标志符号的像素为单位和用来模拟带删除线或下划线某些额外矩形的像素为单位的并集。 不透明的像素为单位定义由不透明的矩形。

**DrvTextOut**选择使用指针，pfo，查询当前的指定的字体[ **FONTOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff565974)结构。 此过程可以包括下载软字体或字体替换或任何其他设备所需的字体优化。

如果驱动程序具有可缩放字体，则应调用[ **FONTOBJ\_pxoGetXform** ](https://msdn.microsoft.com/library/windows/hardware/ff566008)当前 FONTOBJ 结构，以返回关联的字体的名义设备转换函数. 这是必需的驱动程序所提供的字体。 名义上的空间是设备字体的设计空间。 例如，PostScript 字体定义 1000年-1000年单元字符单元格。 度量值中返回的大多数[ **IFIMETRICS** ](https://msdn.microsoft.com/library/windows/hardware/ff567418)结构都将转换为名义上的空间，这就是名义上设备转换是必要的原因。

图形引擎通过调用函数查询驱动程序[ **DrvGetGlyphMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556230)若要了解如何在内部应缓存其字体信息。 它可以缓存单个标志符号位图、 大纲中，或都不 （的正确选择设备字体）。

 

 





