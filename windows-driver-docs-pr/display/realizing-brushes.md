---
title: 意识到画笔
description: 意识到画笔
ms.assetid: e6a7c008-50b2-4411-b8f8-99a3ca99e9f4
keywords:
- GDI WDK Windows 2000 显示模式
- 图形驱动程序 WDK Windows 2000 显示模式
- WDK GDI 模式
- 画笔 WDK GDI
- 源 WDK GDI 画笔
- 意识到 WDK GDI 画笔
- 抖动 WDK Windows 2000 显示
- 抖动 WDK Windows 2000 显示的颜色
- 颜色管理 WDK GDI
- DrvRealizeBrush
- DrvDitherColor
- 图面上画笔模式 WDK GDI
- 填充 WDK GDI
- 行 WDK GDI
- 绘制 WDK GDI，画笔
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58708feb5e26ecd67154d88b0abf114e40bb4992
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534127"
---
# <a name="realizing-brushes"></a>意识到画笔


## <span id="ddk_realizing_brushes_gg"></span><span id="DDK_REALIZING_BRUSHES_GG"></span>


输出行、 文本或填充的图形函数作为自变量需要至少一个画笔。 画笔定义要使用指定的表面上绘制图形对象的模式。 每个输出采用画笔函数需要*画笔源*。 画笔源设备面与画笔的模式的左上角的像素对齐上提供像素的坐标。 画笔图案重复 （平铺） 以涵盖整个设备表面。

该驱动程序可以支持以下函数来定义画笔：

[**DrvRealizeBrush**](https://msdn.microsoft.com/library/windows/hardware/ff556273)

[**DrvDitherColor**](https://msdn.microsoft.com/library/windows/hardware/ff556202)

使用混合模式，用于定义应如何与已在设备图面上的数据混合模式始终使用的画笔。 组合数据类型包括两个 ROP2 值打包到单个 ULONG 值。 前台*ROP*处于最低位字节。 下一个字节包含背景 ROP。 有关详细信息，请参阅 Microsoft Windows SDK 文档。

GDI 跟踪的应用程序已请求使用的所有逻辑画笔。 然后要求驱动程序进行绘制，GDI 首先发出对驱动程序函数的调用[ **DrvRealizeBrush**](https://msdn.microsoft.com/library/windows/hardware/ff556273)。 这样，驱动程序来计算其自己的绘图代码所需模式的最佳表示形式。

*DrvRealizeBrush*调用以实现定义的画笔*psoPattern* （画笔模式） 和*psoTarget* （已实现的画笔的图面）。 已实现的画笔包含驱动程序所需用图案填充区域的信息和加速器。 定义和驱动程序仅使用此信息。 编写驱动程序实现的画笔可能会导致驱动程序并将其分配通过调用 GDI 的缓冲区服务函数[ **BRUSHOBJ\_pvAllocRbrush** ](https://msdn.microsoft.com/library/windows/hardware/ff538263)从内*DrvRealizeBrush*。 GDI 缓存所有已实现的画笔;因此，它们很少需要重新计算。

在中*DrvRealizeBrush*，则**BRUSHOBJ**，或标准格式位图。 对于光栅设备，描述画笔模式的图面表示位图;和对于向量设备，它始终是其中一个返回模式曲面[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)函数。 使用画笔的透明度掩码是一个位每像素位图与模式的相同程度。 零掩码位意味着像素被视为可画笔; 的背景像素也就是说，目标像素不受该特定模式像素。 *DrvRealizeBrush*使用[ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)结构转换中的设备颜色索引到画笔图案的颜色。

该驱动程序应调用 GDI 服务函数[ **BRUSHOBJ\_pvGetRbrush** ](https://msdn.microsoft.com/library/windows/hardware/ff538264)时的值**iSolidColor** BRUSHOBJ 结构中的成员是0xFFFFFFFF 并**pvRbrush**成员是**NULL**。 **BRUSHOBJ\_pvGetRbrush**检索指向指定画笔的驱动程序的实现。 如果画笔不已经实现驱动程序将调用此函数时，会自动调用 GDI *DrvRealizeBrush*的驱动程序的实现的画笔。

### <a name="span-idditheringspanspan-idditheringspanspan-idditheringspandithering"></a><span id="Dithering"></span><span id="dithering"></span><span id="DITHERING"></span>抖色

如有必要，GDI 可以尝试用不能在硬件完全表示一种颜色创建画笔时请求驱动程序的帮助。 GDI 调用驱动程序函数**DrvDitherColor**。

抖色处理使用多种颜色的模式来估计所选的颜色和其结果是一个设备颜色索引的数组。 创建使用模式将这些颜色画笔通常是准确的给定颜色估算。 [**DrvDitherColor** ](https://msdn.microsoft.com/library/windows/hardware/ff556202)还可以表示的设备不能完全指定的颜色。 若要执行此操作， *DrvDitherColor*请求的多个颜色模式并创建一个用于近似于给定的纯色画笔。

该函数*DrvDitherColor*是可选的仅当调用 GCAPS\_颜色\_抖动或 GCAPS\_MONO\_抖动功能标志中设置**flGraphicsCaps**的成员[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构。 *DrvDitherColor*可以返回下表中列出的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DCR_DRIVER</p></td>
<td align="left"><p>指示具有已抖动值计算由驱动程序。 句柄<strong>cxDither</strong>通过<strong>cyDither</strong>设备颜色索引的数组将传回到这种情况。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DCR_HALFTONE</p></td>
<td align="left"><p>指示 GDI 应接近使用现有的设备 （半色调） 调色板的颜色。 例如，GDI 可以为包含三个或四种颜色的打印机使用典型的调色板。 DCR_HALFTONE 可以用于显示驱动程序，仅当设备包含设备 （半色调） 面板中的，如 VGA 16 适配器卡，它具有标准固定的调色板。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DCR_SOLID</p></td>
<td align="left"><p>指示 GDI 应映射到现有设备调色板 （多对一） 中最接近的颜色值的请求的颜色。</p></td>
</tr>
</tbody>
</table>

 

单色驱动程序应支持*DrvDitherColor*使 GDI 能够很好的灰色级模式。

 

 





