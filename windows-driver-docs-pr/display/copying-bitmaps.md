---
title: 复制位图
description: 复制位图
ms.assetid: 76e07c66-7e57-42d7-b6da-c13c8e9a8dee
keywords:
- GDI WDK Windows 2000 显示，位图
- 图形驱动程序 WDK Windows 2000 显示，位图
- 绘制 WDK GDI，位图
- 位图 WDK GDI
- 复制位图
- DrvBitBlt
- DrvCopyBits
- DrvStretchBlt
- DrvTransparentBlt
- 拉伸 WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78bd053c3fa933722e7659b4a8a1939a0500f934
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361409"
---
# <a name="copying-bitmaps"></a>复制位图


## <span id="ddk_copying_bitmaps_gg"></span><span id="DDK_COPYING_BITMAPS_GG"></span>


**位块传输** (由驱动程序实现的 BitBlt) 函数会将位从一个表面复制到另一个表面。 这些函数包括：

[**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)

[**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits)

[**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt)

[**DrvTransparentBlt**](/windows/win32/api/winddi/nf-winddi-drvtransparentblt)

还有一个名为 [**DrvSaveScreenBits**](/windows/win32/api/winddi/nf-winddi-drvsavescreenbits)的显示驱动程序特定的 BitBlt 函数。

如果在上绘制的表面是 *设备管理的图面* 或位图，则驱动程序必须支持最低级别的位块传输函数。 如果图面是 GDI 托管的标准格式位图，则 GDI 仅处理不受驱动程序挂钩的操作。

### <a name="span-iddrvbitbltspanspan-iddrvbitbltspan-drvbitblt"></a><span id="drvbitblt"></span><span id="DRVBITBLT"></span> DrvBitBlt

[**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)函数提供一般位块传输功能。 如果使用了源，则 **DrvBitBlt** 会将源矩形的内容复制到目标矩形。  (此函数的 *pptlSrc* 参数标识矩形的左上角。 ) 如果没有源矩形，则 **DrvBitBlt** 将忽略 *pptlSrc* 参数。 目标矩形（要修改的图面）由两个整数点（左上角和右下角）定义。 矩形 *向右右下角* ;矩形的下边缘和右边缘不是块传输的一部分。 不能使用空目标矩形调用 **DrvBitBlt** 。 矩形的两点始终是正确的，也就是说，右下点的两个坐标都大于左上角中的对应项。

[**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt) 处理不同的 ROPs，并根据设备执行优化。 在某些情况下，如果 ROP 是纯色，则可以执行填充，而不是 BitBlt。 对于不支持 ROPs 的设备或驱动程序，如 Pscript 驱动程序，显示的图像与打印的图像之间可能存在差异。

（可选）可屏蔽由 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt) 处理的块传输，并包含颜色索引转换。 翻译向量有助于调色板的颜色索引翻译。 使用一系列剪辑矩形时，可能需要使用显示驱动程序任意剪裁传输。 所需的区域和信息由 GDI 提供。

实现 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt) 表示编写不具有标准格式 *帧缓冲区* 的光栅显示驱动程序的驱动程序所涉及的重要工作部分。 使用 Windows 驱动程序工具包提供的 Microsoft VGA 驱动程序 (WDK) 提供支持平面设备基本功能的示例代码。 为其他设备实现 **DrvBitBlt** 可能会比较复杂。

### <a name="span-iddrvcopybitsspanspan-iddrvcopybitsspan-drvcopybits"></a><span id="drvcopybits"></span><span id="DRVCOPYBITS"></span> DrvCopyBits

GDI 从其模拟操作调用 [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits) 函数，以便在设备托管的光栅表面和 GDI 标准格式位图之间进行转换。 **DrvCopyBits** 为 SRCCOPY (0xCCCC 提供了快速路径，) ROP 位块传输。

此函数必须与任何标准格式位图之间来回转换驱动因素，这是具有设备托管的位图或光栅图面的图形驱动程序所必需的。 永远不会使用空的目标矩形调用 [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits) ，目标矩形的两个点总是有序排序。 此调用具有与 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)相同的要求。

如果驱动程序支持设备管理的图面或位图，则驱动程序必须实现 [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits) 函数。 在调用 **DrvCopyBits** 时，驱动程序至少必须执行以下操作：

-   执行与位图、设备首选格式和设备图面之间的块传输。

-   通过 SRCCOPY (0xCCCC) *光栅操作 (ROP)* 执行传输。

-   允许任意剪裁。

驱动程序可以使用 GDI [**CLIPOBJ**](/windows/win32/api/winddi/ns-winddi-clipobj) 枚举服务来减少对一系列剪辑矩形的剪辑。 GDI 向下传递翻译向量（ [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-xlateobj) 结构），以帮助在源和目标曲面之间进行颜色索引转换。

如果设备表面被组织为标准格式的与 *设备无关的位图 (DIB)* ，则驱动程序只能支持简单传输。 如果调用的是一个复杂的 ROP，则驱动程序可以通过调用 [**EngCopyBits**](/windows/win32/api/winddi/nf-winddi-engcopybits) 函数来使阻止传输请求返回到 GDI。 这允许 GDI 将调用分解为驱动程序可以执行的更简单的函数。

[**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits) 也是通过 RLE 位图调用的 (参阅 Microsoft Windows SDK 文档) 和 **设备相关位图 (DDBs)** 。 由于应用程序调用了多个 Win32 GDI 例程，因此会将位图提供给此函数。 可选的 DDB 仅受几个专用驱动程序支持。

### <a name="span-iddrvstretchbltspanspan-iddrvstretchbltspan-drvstretchblt"></a><span id="drvstretchblt"></span><span id="DRVSTRETCHBLT"></span> DrvStretchBlt

驱动程序可以选择提供 [**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt) 函数，甚至还可以提供支持设备管理的图面的驱动程序。 此函数为设备管理的和 GDI 管理的图面之间的拉伸块传输提供功能。 **DrvStretchBlt** 仅支持某些类型的拉伸，如使用整数倍数拉伸。

[**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt) 还允许驱动程序在 GDI 位图上写入，特别是当驱动程序可以执行半色调操作时。 函数还允许将相同的半色调算法应用于 GDI 位图和设备图面。

[**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt) 将几何源矩形精确地映射到几何目标矩形。 源是一个矩形，其中的角从给定的整数坐标 (-0.5，-0.5) 。 函数参数中指定的点位于与像素中心对应的整数坐标。 由两个这类点定义的矩形被视为几何，其中两个顶点的坐标是给定点，但从每个坐标中减去了0.5。  (GDI [**POINTL**](/windows/win32/api/windef/ns-windef-pointl) 结构使用简写表示法来指定这些小数坐标顶点。 ) 请注意，任何此类矩形的边缘永远不会与像素相交，但会绕一组像素。 该矩形内的像素是下右排边框的普通像素。

定义源矩形角的点具有序顺序;不能为 [**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt) 提供空的源矩形。 与 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)不同，可以使用单个剪辑矩形调用 **DrvStretchBlt** ，以防止剪裁输出时出现舍入错误。

目标矩形由两个整数点定义。 这些点不会有序排序，这意味着第二个点的坐标并不一定大于第一个点的坐标。 这些点所描述的源矩形不包括下边缘和右边缘。 由于此矩形的顺序不正确， [**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt) 有时必须在两个 x 坐标和/或两个 y 坐标中执行倒置。  (驱动程序不得尝试读取不在源图面) 上的像素。 不能使用空目标矩形调用 **DrvStretchBlt** 。

对于颜色转换， [**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt)向 [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-xlateobj)结构提供一个指针 *pxlo* ，用于在源和目标曲面之间进行转换。 可以查询 XLATEOBJ 结构来查找任何源索引的目标索引。 对于高质量拉伸块传输，在某些情况下需要 **DrvStretchBlt** 来插入颜色。 **DrvStretchBlt** 还使用 COLORADJUSTMENT 结构定义要在延伸位之前应用于源位图的颜色调整值。

[**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt) 使用 *iMode* 参数定义要将源像素合并为输出的方式。 特别是， *iMode* 提供了半色调选项，该选项允许驱动程序使用输出图面中的像素组来接近输出的颜色或灰色级别。 对 COLORADJUSTMENT 结构所做的更改将在下一次 **DrvStretchBlt** 调用后传递给驱动程序， *IMODE* 为半色调。 此外，如果驱动程序需要 GDI 来处理 GDI 位图的半色调，则驱动程序将 **DrvStretchBlt** ，将 *iMode* 参数设置为半色调，并将其返回 [**EngStretchBlt**](/windows/win32/api/winddi/nf-winddi-engstretchblt)。

如果 [**DrvStretchBlt**](/windows/win32/api/winddi/nf-winddi-drvstretchblt) 已将调用挂钩到 [**EngStretchBlt**](/windows/win32/api/winddi/nf-winddi-engstretchblt) 函数并要求其执行不支持的操作，则它会将请求返回到 GDI，以便适当的函数可以处理它。

### <a name="span-iddrvtransparentbltspanspan-iddrvtransparentbltspan-drvtransparentblt"></a><span id="drvtransparentblt"></span><span id="DRVTRANSPARENTBLT"></span> DrvTransparentBlt

[**DrvTransparentBlt**](/windows/win32/api/winddi/nf-winddi-drvtransparentblt)函数导致将源位图复制到目标位图，使目标位图的部分在复制后保持可见。 此函数的 *iTransColor* 参数指定要成为透明的颜色。

下图描绘了透明 blt 的示例。

![阐释透明 blt 的示意图](images/transblt.png)

在从左到右的位置上，上图显示了在透明的 blt 之前的源位图、目标位图和透明 blt 之后的目标位图。 请注意， *iTransColor* 中的颜色与以下四个区域中的颜色相同：下面的四个区域和源位图中中央区域的两侧。

发生 blt 操作时，不会复制这四个区域，这将导致这些区域下的目标位图中的任何像素模式保持可见。 其他区域下的任何像素模式 (四个角，而中心) 在透明 blt 中被覆盖。

这在最右侧的图像中进行了说明：四个角部分中字母 "m" 的部分，并覆盖了源位图中的颜色。 字母 "m" 的四个区域的颜色与 *iTransColor* 中的颜色相同。

