---
title: 混合内存分配
description: 混合内存分配
ms.assetid: 171efa48-bd1e-4545-a5c2-0b3ad4383448
keywords:
- 混合的内存分配 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9740f8f9877d7d01e79e2b93a67e6c62247d9341
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358415"
---
# <a name="mixed-memory-allocation"></a>混合内存分配


## <span id="ddk_mixed_memory_allocation_gg"></span><span id="DDK_MIXED_MEMORY_ALLOCATION_GG"></span>


线性和矩形内存堆可以进行混合和匹配以任何方式，如果硬件支持。 例如，如果前台缓冲区已固定的间距，支持 DirectDraw 的驱动程序可以分配右侧矩形堆。

下图中所示，如果保留足够内存以主面下方，可以向用于后台缓冲区的线性堆进行这一领域。

![关系图演示如何混合的内存分配](images/ddfig6.png)

上图显示了线性一部分主要面 (堆 1) 下的内存和矩形一部分由主图面 (堆 2) 右侧的 DirectDraw 回收的内存。

下面的伪代码演示如何[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构混合的线性和矩形的内存的设置：

```cpp
/*
 * video memory pool usage
 */
static VIDEOMEMORY vidMem [] =
{
  { VIDMEM_ISRECTANGULAR, 0x00000000, 0x00000000,
            { 0 }, { 0 } },
  { VIDMEM_ISLINEAR, 0x00000000, 0x00000000,
            { 0 }, { 0 } },
};
```

可以在此实例中分配的显示内存的两个方面。 主图面的概念的右侧区域是一定矩形，将由 VIDMEM\_ISRECTANGULAR 标志。 从概念上讲以下主表面区域可以是线性的并且由 VIDMEM\_ISLINEAR 标志。

下面的伪代码演示如何混合使用线性和矩形设置堆的内存：

```cpp
/*
 * video memory pool information
 */

/* set up the pointer to the first available video memory after the primary surface */
    ddHALInfo.vmiData.pvmList       = vidMem;

/* how many heaps are there   
     ddHALInfo.vmiData.dwNumHeaps       = 2;

/* The linear piece:  */


/*
 * remainder of screen memory
 */

    VideoHeapBase = ddHALInfo.vmiData.fpPrimary + dwPrimarySurfaceSize
                    + dwCacheSize;
    VideoHeapEnd = VideoHeapBase + dwDDOffScreenSize - 1;
    vidMem[0].fpStart = VideoHeapBase;
    vidMem[0].fpEnd = VideoHeapEnd;

/* The rectangular piece:  */

/* set up the pointer to the next available video memory */
    ddHALInfo.vmiData.pvmList     = vidMem[1];

/*
 *  Compute the Pitch here ...
 */

    vidMem[1].fpStart  = ddHALInfo.vmiData.fpPrimary + 
                        dwPrimarySurfaceWidth;
    vidMem[1].dwWidth  = dwPitch - dwPrimarySurfaceWidth;
    vidMem[1].dwHeight = dwPrimarySurfaceHeight;
    vidMem[1].ddsCaps.dwCaps = 0;  // surface has no use restrictions
```

通过确定起点和终点的主图面，下面的暂存区域设置线性内存堆为由**fpStart**并**fpEnd**成员的线性[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构 (<strong>vidMem\[</strong>0<strong>\]</strong>)。 矩形部分设置使用的起始点，由**fpStart**矩形 VIDEOMEMORY 结构中的成员 (<strong>vidMem\[</strong>1 <strong>\]</strong>)，宽度，由**dwWidth**成员和高度，指示**dwHeight**成员的主图面。 间距 ( **dwPitch**成员) 可以设置的矩形部分之前，必须计算。 这是与矩形的上一示例中，相同间距是而不是第一个 VIDEOMEMORY 结构的第二个元素的这种情况下除外。 每个新堆需要新的 VIDEOMEMORY 结构。

在某些情况下，翻转注册可以处理仅 256 KB 边界。 在这些情况下，小型堆可以使用的缓存中的下边框和后台缓冲区，允许后台缓冲区，以从 256 KB 边界开始的开始之间的空白区域。 此示例中未显示，但它可以通过向 VIDEOMEMORY 结构中添加另一个元素并设置刚超出缓存的起始点和之前的 256 KB 边界的结束位置的实现。 此类堆应标记为 DDSCAPS\_后台缓冲区，因此它可以跳过，当堆管理器查找后台缓冲区。 此后台缓冲区堆 （一个对齐） 也将标记与 DDSCAPS\_OFFSCREENPLAIN 以防止使用该堆，直到没有其他内存在普通的屏外表面其他堆中提供子画面和纹理。

 

 





