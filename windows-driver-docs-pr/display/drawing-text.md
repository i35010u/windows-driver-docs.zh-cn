---
title: 绘制文本
description: 绘制文本
ms.assetid: e5bf4673-93c4-4cc5-b74d-e0e3a487ec3d
keywords:
- GDI WDK Windows 2000 显示，文本输出
- 图形驱动程序 WDK Windows 2000 显示，文本输出
- 文本输出 WDK 图形
- DrvTextOut
- DrvGetGlyphMode
- 表面文本输出 WDK GDI
- GDI WDK Windows 2000 显示、文本输出、绘制
- 图形驱动程序 WDK Windows 2000 显示、文本输出、绘制
- 绘制文本 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3184e00f315bee2762e086df7bec073dabfc524d
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91424040"
---
# <a name="drawing-text"></a>绘制文本


## <span id="ddk_drawing_text_gg"></span><span id="DDK_DRAWING_TEXT_GG"></span>


仅对 *设备管理的图面* (设备位图或图面) ，或如果驱动程序已在 [**EngAssociateSurface**](/windows/win32/api/winddi/nf-winddi-engassociatesurface) 函数中挂接了调用，则仅对设备管理的图面调用文本输出函数。 文本的图形输出基元是函数：

[**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout)

[**DrvGetGlyphMode**](/windows/win32/api/winddi/nf-winddi-drvgetglyphmode)

GDI 调用 **DrvTextOut** 来呈现文本输出的指定位置的一组标志符号的像素。 许多**DrvTextOut**功能都是使用[**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)函数返回的[**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-tagdevinfo)结构的 GCAPS 位来定义的。

**DrvTextOut**的输入参数定义了两组像素：*前景*和不*透明*。 驱动程序呈现图面以提供以下结果：

1.  不透明像素首先呈现，不透明画笔。

2.  然后，将用前景画笔呈现前景像素。

其中每个渲染操作都在 *剪辑区域*中执行。 剪辑区域外的像素不会受到影响。

驱动程序必须呈现图面，以便在表面上首先使用不透明画笔计算并绘制不透明像素。 然后，使用前台画笔来计算和渲染前景像素。 其中每个操作都受剪辑限制。

前景和不透明像素组成了一个掩码，通过它可以将颜色刷到表面上。 字体的字形本身不具有颜色。 前景像素组定义为标志符号像素的并集，以及用于模拟删除线或下划线的某些额外矩形的像素。 不透明像素由不透明矩形定义。

**DrvTextOut** 使用指针 pfo 选择指定的字体，以查询当前 [**FONTOBJ**](/windows/win32/api/winddi/ns-winddi-fontobj) 结构。 此过程可能包括下载软字体或字体替换或设备所需的任何其他字体优化。

如果驱动程序具有可缩放字体，则它应为当前 FONTOBJ 结构调用 [**FONTOBJ \_ pxoGetXform**](/windows/win32/api/winddi/nf-winddi-fontobj_pxogetxform) 函数，以返回关联字体的名义到设备转换。 这对于驱动程序提供的字体是必需的。 名义空间是设备字体的设计空间。 例如，PostScript 字体在 1000 x 1000 单元字符单元中定义。 [**IFIMETRICS**](/windows/win32/api/winddi/ns-winddi-ifimetrics)结构中返回的大部分指标都转换为名义空间，这就是需要进行名义到设备转换的原因。

图形引擎通过调用函数 [**DrvGetGlyphMode**](/windows/win32/api/winddi/nf-winddi-drvgetglyphmode) 来查询驱动程序，以了解它如何在内部缓存其字体信息。 它可以将单独的字形缓存为位图、轮廓，或者两者都不 () 的设备字体的正确选择。

 

