---
title: 矩形内存分配
description: 矩形内存分配
keywords:
- 矩形内存分配 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e49701485d4143aae223dd349e8e6cd9032990b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810081"
---
# <a name="rectangular-memory-allocation"></a>矩形内存分配


## <span id="ddk_rectangular_memory_allocation_gg"></span><span id="DDK_RECTANGULAR_MEMORY_ALLOCATION_GG"></span>


每次将间距固定到给定堆中的所有图面的特定大小时，显示内存被视为 *矩形* 。

使用矩形显示内存时，布局为二维，具有有限的宽度和高度。 此宽度并非始终与屏幕宽度相同。 因为 "显示内存" 必须考虑不同的显示分辨率和设计注意事项，所以，实际水平宽度可能跨越比当前在监视器上显示的内容大得多的区域。 如内存堆分配中所述，螺距值基于要添加到显示内存列中的字节数，以便在以下扫描行上到达同一列显示内存。

例如，尽管屏幕可能会在一屏上显示640像素，如果矩形显示内存在8位像素之间为1280字节，则音调为 1280 (不是 640) 。 使用16位像素跨1280像素水平拉伸的跨度为2560。 32位像素的跨度是8位像素的四倍，因此，如果显示在跨的 1280 32 位像素，则音调为5120。

通常，应用程序比线性内存更有效地使用矩形内存，因为在应用程序存储大型表面后小片段可能会保留。 即使剩余空间中的可用字节数大于任何新的图面要求，应用程序也可能无法在剩余空间中存储其他表面。 应用程序可以在第一次提供的基础上访问这一空间，并且只能存储可容纳剩余片段的小表面。

矩形堆最大可以为可用内存的连续区域，但不能为 L 形，因为其大小是按 X X Y 坐标度量的。 如果矩形堆的高度不够并且宽度足以容纳主图面，则它不能是后台缓冲区。 如果主要表面的跨度不等于主图面的显示宽度，则显示在下图中的 (堆 1) 的矩形内存块将保留在下图中。 此块的宽度与间距减去显示宽度的宽度相同。 如果现有的显示驱动程序采用固定的间距，则在线性卡中也可能会出现适当的剩余内存。 矩形或线性内存也可以在主表面 (下面，但在此示例中不能) 。

下图说明了矩形内存分配。

![阐释矩形内存分配的关系图](images/ddfig5.png)

在上图中，通过将主图面的宽度添加到主表面的起始地址来计算矩形堆的 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory)结构) 的 **fpStart** 成员指定的 (起点。 还会计算宽度和高度，以给出矩形堆的尺寸。 如果任何内存仍低于 Windows 缓存，则可以在此处创建一个堆。

下面的伪代码演示如何为矩形内存设置 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory) 结构：

```cpp
/*
 * video memory pool usage
 */
static VIDEOMEMORY vidMem [] = {
    { VIDMEM_ISRECTANGULAR, 0x00000000, 0x00000000,
           { 0 }, { 0 } },
};
```

矩形内存的代码与其线性对应项之间唯一的区别是 VIDMEM \_ ISRECTANGULAR 标志，指示这是矩形内存

以下伪代码显示了如何设置矩形内存堆：

```cpp
/*
 * video memory pool information
 */

/* set up the pointer to the first available video memory after the primary surface */
    ddHALInfo.vmiData.pvmList      = vidMem;

/* this is set to zero because there may only be one heap depending on the pitch 
    ddHALInfo.vmiData.dwNumHeaps      = 0; 


/*
 *  Compute the Pitch here ...
 */


    vidMem[0].fpStart  = ddHALInfo.vmiData.fpPrimary + dwPrimarySurfaceWidth;
    vidMem[0].dwWidth  = dwPitch - dwPrimarySurfaceWidth;
    vidMem[0].dwHeight = dwPrimarySurfaceHeight;
    vidMem[0].ddsCaps.dwCaps = 0;      // surface has no use restrictions
```

内存堆起点设置为主表面的起始地址加上主图面的宽度。 宽度由间距减去主图面的宽度来确定。 高度设置为主要表面的高度。 Surface 功能设置为零，以指示没有施加的曲面使用限制 (因此，该图面可用于 sprite 或任何其他类型的图面) 。

 

