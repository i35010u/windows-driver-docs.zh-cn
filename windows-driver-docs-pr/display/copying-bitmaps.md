---
title: 复制位图
description: 复制位图
ms.assetid: 76e07c66-7e57-42d7-b6da-c13c8e9a8dee
keywords:
- GDI WDK Windows 2000 显示位图
- 图形驱动程序 WDK Windows 2000 显示位图
- 绘制 WDK GDI，位图
- WDK GDI 位图
- 复制位图
- DrvBitBlt
- DrvCopyBits
- DrvStretchBlt
- DrvTransparentBlt
- 拉伸 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41605aa7a8ae56e2e6131927396d67d139917576
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391282"
---
# <a name="copying-bitmaps"></a>复制位图


## <span id="ddk_copying_bitmaps_gg"></span><span id="DDK_COPYING_BITMAPS_GG"></span>


**位块传输**实现由驱动程序复制到另一个图面中的位块 (BitBlt) 函数。 这些功能包括：

[**DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)

[**DrvCopyBits**](https://msdn.microsoft.com/library/windows/hardware/ff556182)

[**DrvStretchBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556302)

[**DrvTransparentBlt**](https://msdn.microsoft.com/library/windows/hardware/ff557283)

此外，还有一个名为的特定于驱动程序显示 BitBlt 函数[ **DrvSaveScreenBits**](https://msdn.microsoft.com/library/windows/hardware/ff556278)。

如果在图面上进行绘制*设备管理面*或位图，该驱动程序必须支持最低级别的位块传输函数。 如果在图面是 GDI 托管标准格式位图，GDI 处理驱动程序通过不挂起操作。

### <a name="span-iddrvbitbltspanspan-iddrvbitbltspan-drvbitblt"></a><span id="drvbitblt"></span><span id="DRVBITBLT"></span> DrvBitBlt

[ **DrvBitBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556180)函数提供了常规位块传送功能。 如果使用的源**DrvBitBlt**将复制到目标矩形上的源矩形的内容。 ( *PptlSrc*此函数的参数标识的矩形的左上的角。)如果没有源矩形**DrvBitBlt**会忽略*pptlSrc*参数。 目标矩形，要修改的面定义的两个整数点，左上角和右下角。 矩形*较低的右侧排他*; 较低和右边缘的矩形的不是块传输的一部分。 **DrvBitBlt**不能调用一个空的目标矩形。 两个点的矩形的很好地进行排序;也就是说，这两个坐标的右下方是点的大于其左上角的点中的匹配。

[**DrvBitBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556180)处理不同 ROPs 和执行优化，具体取决于设备。 在某些情况下，如果 ROP 是纯色，填充而不是 BitBlt 可以执行。 对于设备或不支持 ROPs，如 Pscript 驱动程序的驱动程序，可以有差异的显示和打印图像之间。

（可选） 块传输由[ **DrvBitBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556180)可以屏蔽，并涉及颜色索引转换。 转换向量帮助的调色板颜色索引转换。 传输可能会需要任意剪辑显示驱动程序，通过使用一系列的剪辑矩形。 通过 GDI 均提供了所需的区域和信息。

实现**DrvBitBlt**。 提供使用 Windows Driver Kit (WDK) 的 Microsoft VGA 驱动程序提供了平面数据的设备支持的基本功能的示例代码。 实现**DrvBitBlt**其他设备可能不太复杂。

### <a name="span-iddrvcopybitsspanspan-iddrvcopybitsspan-drvcopybits"></a><span id="drvcopybits"></span><span id="DRVCOPYBITS"></span> DrvCopyBits

[ **DrvCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff556182)通过 GDI 从设备管理光栅图面和 GDI 标准格式位图之间进行转换其模拟操作调用函数。 **DrvCopyBits** SRCCOPY (0xCCCC) ROP 位块传输提供的快速路径。

所需的图形驱动程序和设备管理位图或光栅图面，则必须将此函数转换驱动程序图面与任何标准格式的位图。 [**DrvCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff556182)从来不是一个空的目标矩形，并很好地排序目标矩形的两个点。 此调用具有相同的要求[ **DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)。

如果驱动程序支持的设备管理面或位图，该驱动程序必须实现[ **DrvCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff556182)函数。 该驱动程序必须在最低限度上，执行以下操作时**DrvCopyBits**调用：

-   执行块传输到和从位图，设备的首选格式，并且设备表面。

-   执行与 SRCCOPY (0xCCCC) 传输*光栅操作 (ROP)*。

-   允许任意剪辑。

该驱动程序可以使用 GDI [ **CLIPOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff539417)枚举服务降低了一系列的剪辑矩形剪辑。 向下转换矢量，将传递 GDI [ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)结构，以帮助在源和目标的图面之间的颜色索引转换中。

如果作为标准格式组织的设备面*独立于设备的位图 (DIB)*，该驱动程序可以支持简单的传输。 如果使用复杂 ROP 传入的调用，驱动程序可以回通过调用 GDI 被迫块传输请求[ **EngCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff564196)函数。 这使 GDI 分解到驱动程序可以执行的更简单函数的调用。

[**DrvCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff556182)也称为使用 RLE 位图 （请参阅 Microsoft Windows SDK 文档） 和**设备相关位图 (Ddb)**。 由于多个 Win32 GDI 例程的应用程序程序调用此函数提供位图。 可选 DDB 仅受几个专用驱动程序。

### <a name="span-iddrvstretchbltspanspan-iddrvstretchbltspan-drvstretchblt"></a><span id="drvstretchblt"></span><span id="DRVSTRETCHBLT"></span> DrvStretchBlt

（可选） 可以提供一个驱动程序[ **DrvStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556302)函数，甚至支持设备管理 surface 驱动程序。 此函数提供了用于拉伸设备管理和 GDI 管理界面之间的块传输功能。 **DrvStretchBlt**仅支持某些类型的延伸，如拉伸由整数倍数。

[**DrvStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556302)还允许在 GDI 位图上编写，尤其是在驱动程序可以执行半色调的驱动程序。 该函数还允许相同的半色调算法，若要应用于 GDI 位图和设备表面。

[**DrvStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556302)映射到一个几何目标矩形上完全几何源矩形。 源是一个具有移置开的边角的矩形 （-0.5，-0.5） 从给定的整数坐标。 函数参数中指定的点之间的整数坐标为对应于像素中心上。 通过此类的两个点定义的矩形被视为可几何，有两个顶点坐标的给定的点，但使用 0.5 减去每个协调。 (GDI [ **POINTL** ](https://msdn.microsoft.com/library/windows/hardware/ff569166)结构使用简写表示法来指定这些坐标顶点，小数部分。)请注意这种矩形的边缘永远不会相交像素，但会围绕一组的像素为单位。 在矩形内的像素是较低的右侧排他矩形正常像素。

定义源矩形的角点都秩序井然;[ **DrvStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556302)不能有一个空的源矩形。 与不同[ **DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)， **DrvStretchBlt**可以调用与要防止在输出中的剪辑舍入误差的单个剪辑矩形。

由两个整数点定义目标矩形。 这些点都不秩序井然，这意味着，第二个点的坐标不一定比第一个更大。 这些点描述了源矩形不包括较低和右边缘。 矩形还未排序，因为[ **DrvStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556302)有时必须反转执行两个 x 坐标和/或两个 y 坐标。 （该驱动程序必须不尝试读取不存在源图面的像素为单位）。 **DrvStretchBlt**不能调用一个空的目标矩形。

颜色翻译[ **DrvStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556302)提供一个指针*pxlo*到[ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)结构，它使用源和目标的图面之间进行转换。 XLATEOBJ 结构可以通过查询来查找任何源索引的目标索引。 高质量延伸块传输， **DrvStretchBlt**需执行内插在某些情况下的颜色。 **DrvStretchBlt**还使用 COLORADJUSTMENT 结构来定义位将被拉伸之前要应用到源位图的颜色调整值。

[**DrvStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556302)使用*iMode*参数来定义如何对源像素将合并为输出。 具体而言， *iMode*提供允许驱动程序以使用输出图面中的像素为单位的组来近似输出的颜色或灰级别的半色调选项。 COLORADJUSTMENT 结构的变更传递给驱动程序之后的下一步**DrvStretchBlt**使用调用*iMode*的半色调。 此外，如果该驱动程序需要处理 GDI 位图的半色调的 GDI，驱动程序挂钩出**DrvStretchBlt**，设置*iMode*半色调，参数并返回它在[ **EngStretchBlt**](https://msdn.microsoft.com/library/windows/hardware/ff565025)。

如果[ **DrvStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff556302)已挂钩调用[ **EngStretchBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff565025)函数并要求进行操作不支持，它返回到 GDI 请求，以便适当的函数可以处理它。

### <a name="span-iddrvtransparentbltspanspan-iddrvtransparentbltspan-drvtransparentblt"></a><span id="drvtransparentblt"></span><span id="DRVTRANSPARENTBLT"></span> DrvTransparentBlt

[ **DrvTransparentBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff557283)函数导致的源位图复制到目标位图上，这样，目标位图的部分复制后保持可见。 *ITransColor*此函数的参数指定是要进行透明的颜色。

下图描绘了透明 blt 的示例。

![说明透明 blt 的关系图](images/transblt.png)

从左到右上, 图显示了源位图、 透明 blt 之前目标位图和目标位图后透明 blt。 请注意，中的颜色*iTransColor*是相同的上述四个区域中、 下、 左、 向中央区域中的源位图的两端。

Blt 操作发生时，这些四个区域不会复制，这将导致在这些区域为保持可见目标位图中任何像素模式。 在其他区域 （四个角和中心） 下的任何像素模式将透明 blt 中被覆盖。

这最右边的图中所示： 字母的部分是中的四个角和中心覆盖了与中的源位图的颜色。 字母的部分是在四个区域的颜色是中的相同*iTransColor*保持可见。

 

 





