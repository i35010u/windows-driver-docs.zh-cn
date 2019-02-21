---
title: 矩形的内存分配
description: 矩形的内存分配
ms.assetid: 27e60130-3a6e-410a-86a7-19acad5ecb53
keywords:
- 矩形的内存分配 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 771eb07b14039e986bb71780aab07d3a5426010b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540623"
---
# <a name="rectangular-memory-allocation"></a>矩形的内存分配


## <span id="ddk_rectangular_memory_allocation_gg"></span><span id="DDK_RECTANGULAR_MEMORY_ALLOCATION_GG"></span>


显示将内存视为*矩形*每当间距固定为特定大小对于给定的堆中的所有图面。

使用矩形显示内存布局是二维效果，使用有限的宽度和高度。 此宽度并不总是与屏幕的宽度相同。 显示内存必须考虑不同的显示分辨率和设计注意事项，因为实际的水平宽度可能会跨越较大区域比显示器上当前显示的内容。 中所述内存堆分配，pitch 值取决于要添加的列的显示内存以达到以下扫描线上的显示内存的相同列的字节数。

例如，即使屏幕，显示 640 像素，如果矩形显示内存使用 8 位像素跨 1280 字节，pitch 是 1280 (不 640)。 在使用 16 位像素为 1280年像素水平拉伸之间的间距是内存的 2560年。 32 位像素间距是翻 8 位像素，什么是显示是否跨 1280年 32 位像素，pitch 是 5120。

矩形通常使用效率较低的内存比线性内存的应用程序因为应用程序存储的大型图面后，可能会保持小片段。 应用程序可能无法在剩余的空间中存储其他表面，即使在剩余的空间中的可用字节数大于任何新的图面需要。 应用程序可以访问此空间根据第一个来先来先服务的原则，并且只存储在剩余的段中的小图面，适合。

矩形堆可以是可用内存的相邻区域一样大，但不是能为 L 形由于其大小的单位 X 的 Y 坐标。 如果矩形的堆无法足够高，足够宽，用于保存主图面上，它不能为后台缓冲区。 如果主表面的音调不等于主表面的显示宽度，则内存右侧显示的概念是矩形块留下 (如下图中的堆 1)。 这种块是宽度为显示宽度减去间距。 如果现有的显示器驱动程序假定固定的间距，右侧的剩余内存也可能发生线性卡中。 矩形或线性内存可能还会保留在主面下 （但不是在此示例中）。

下图说明了矩形的内存分配。

![说明矩形的内存分配的关系图](images/ddfig5.png)

在上图的起始点 (由**fpStart**的成员[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构) 的矩形堆通过添加计算主表面的起始地址的主要面的宽度。 此外将宽度和高度计算以便矩形堆的维度。 如果任何内存保持低于 Windows 缓存，可能那里创建堆。

下面的伪代码演示如何[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构为矩形的内存设置：

```cpp
/*
 * video memory pool usage
 */
static VIDEOMEMORY vidMem [] = {
    { VIDMEM_ISRECTANGULAR, 0x00000000, 0x00000000,
           { 0 }, { 0 } },
};
```

矩形内存中的代码和对应的线性之间唯一的区别是 VIDMEM\_ISRECTANGULAR 标志以指示这是矩形内存

下面的伪代码显示了如何矩形设置堆的内存：

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

内存堆起始点设置为主表面的起始地址加上主表面的宽度。 宽度取决于主表面的宽度减去间距。 高度设置为主表面的高度。 图面上的功能设置为零以指示没有任何强加的图面上使用限制 （因此，在图面可以使用 sprite 或任何其他类型的图面）。

 

 





