---
title: 混合内存分配
description: 混合内存分配
ms.assetid: 171efa48-bd1e-4545-a5c2-0b3ad4383448
keywords:
- 混合内存分配 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3123dd0a80d310bf5ab9975d902de3c8b211b1e7
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423556"
---
# <a name="mixed-memory-allocation"></a>混合内存分配


## <span id="ddk_mixed_memory_allocation_gg"></span><span id="DDK_MIXED_MEMORY_ALLOCATION_GG"></span>


如果硬件支持线性和矩形内存堆，则可以通过任何方式对其进行混合和匹配。 例如，如果前台缓冲区具有固定的跨度，则支持 DirectDraw 的驱动程序可以在其右侧分配矩形堆。

如下图所示，如果有足够的内存保持在主图面下面，则可以将此区域变成可用于后台缓冲区的线性堆。

![说明混合内存分配的关系图](images/ddfig6.png)

上图显示了在主图面下面 (堆 1) 的线性内存，以及由 DirectDraw 从主表面 (堆 2) 右侧回收的矩形内存块。

下面的伪代码演示如何为混合的线性和矩形内存设置 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory) 结构：

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

在此实例中，可以分配两个显示内存区域。 主图面的概念右侧的区域一定是矩形，并由 VIDMEM \_ ISRECTANGULAR 标志指示。 主要表面下面的区域可以是线性的，由 VIDMEM \_ ISLINEAR 标志指示。

以下伪代码显示了如何设置混合的线性和矩形内存堆：

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

通过确定由线性[**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory)结构的 " **fpStart** " 和 " **fpEnd** " 成员指示的 "线性内存堆" 的起点和终点来设置线性内存堆 (<strong> \[ vidMem</strong>0 <strong>\]</strong>) 。 矩形块是使用起点设置的，由矩形 VIDEOMEMORY 结构的**fpStart**成员指示 (<strong> \[ vidMem</strong>1 <strong>\]</strong>) ，width，由**dwWidth**成员指示，高度由主图面的**dwHeight**成员指示。 在设置矩形部分之前，必须先计算 **dwPitch** 成员)  (间距。 这与上一个矩形示例相同，不同之处在于，这种情况下，螺距是 VIDEOMEMORY 结构的第二个元素，而不是第一个元素。 每个新堆都需要一个新的 VIDEOMEMORY 结构。

在某些情况下，反向寄存器只能处理 256 KB 边界。 在这些情况下，小堆可以占用缓存底部与后台缓冲区开头之间的空间，以允许后台缓冲区在 256 KB 边界处开始。 此示例并未显示，但可以通过将另一个元素添加到 VIDEOMEMORY 结构，并将起点设置为紧靠超过 256 KB 边界之前的缓存和结束点来实现。 此类堆应使用 DDSCAPS 后台缓冲区进行标记， \_ 以便在堆管理器查找后台缓冲区时可以跳过它。 此后台缓冲区堆 (一个对齐的) 也将标记为 DDSCAPS \_ OFFSCREENPLAIN，以防止子画面和纹理使用此堆，直到其他堆中没有可用于屏幕上的无格式表面的其他内存为止。

 

