---
title: 线性内存分配
description: 线性内存分配
keywords:
- 线性内存分配 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cb2bfc91f34a00dc08335ee2ef695a907501f64
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830647"
---
# <a name="linear-memory-allocation"></a>线性内存分配


## <span id="ddk_linear_memory_allocation_gg"></span><span id="DDK_LINEAR_MEMORY_ALLOCATION_GG"></span>


每当可以更改间距以匹配图面宽度时，显示内存将被视为 *线性* ，并考虑对齐要求 (如下图所示) 。 例如，如果 blitter 只能达到8字节的进步，并使用了31像素的动画，则每个显示的行都需要进行调整，以便在8字节边界上对齐下一行。

音调是通过将像素深度（以字节为单位）与图面宽度相乘来确定的，其中考虑了对齐要求。 如果显示范围为 640 8 位像素，则音调为640。 如果像素为16位 (2 个字节) 并且存在 640 X 480 屏幕，则音调为 1280 (640 \* 2) 。 同样，640宽、32位 (4 个字节) 像素屏幕 \* 在线性显示内存中有 2560 (640 4) 。

下图说明了具有一个主表面和一个空闲区的线性内存堆分配。

![阐释线性内存堆分配的关系图](images/ddfig4.png)

指向主图面的开头的指针是 **fpPrimary**（ [**VIDEOMEMORYINFO**](/windows/win32/api/ddrawint/ns-ddrawint-videomemoryinfo) 结构的成员）。 主要表面和各种 Windows 缓存的大小将添加到此，以指定指向草稿区域开头的指针，由 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory)结构的 **fpStart** 成员指示。 由 **VIDEOMEMORY** 结构的 **fpEnd** 成员指示的终结点是通过添加剩余内存的大小减一来计算的。

[**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory)结构包含管理显示内存堆的信息。 此示例在 **VIDEOMEMORY** 结构数组中只有一个元素，因为只有一个堆。 VIDMEM \_ ISLINEAR， **VIDEOMEMORY** 结构的 **dwFlags** 成员中的标志将此标记表示为线性内存。

以下伪代码显示如何为线性内存设置 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory) 结构：

```cpp
/*
 * video memory pool usage
 */
static VIDEOMEMORY vidMem [] = {
    { VIDMEM_ISLINEAR, 0x00000000, 0x00000000,
           { 0 }, { 0 } },
};/*
```

以下伪代码显示了如何设置线性内存堆：

```cpp
/*
 * video memory pool information
 */

/* Calculate the number of video memory heaps */
    ddHALInfo.vmiData.dwNumHeaps = sizeof ( vidMem ) / sizeof ( vidMem [ 0 ] );

/* set up the pointer to the first available video memory after the primary surface */
    ddHALInfo.vmiData.pvmList     = vidMem;

/*
 * remainder of screen memory
 */

    VideoHeapBase = ddHALInfo.vmiData.fpPrimary + dwPrimarySurfaceSize + dwCacheSize;
    VideoHeapEnd = VideoHeapBase + dwDDOffScreenSize - 1;

    vidMem[ 0 ].fpStart = VideoHeapBase;
    vidMem[ 0 ].fpEnd = VideoHeapEnd;
```

第一个可用草稿区域的开头是通过将 GDI 主图面的开头添加到主表面的大小以及 Windows 画笔、笔和 VDD 缓存的大小来计算的。 该结果用于将 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory) 结构的第一个元素中的起始点设置为空闲区的开头。

可以通过将草稿区域的开头添加到空闲区的大小来查找空闲区的结尾，并将其减去一，使其包含在内。 结果用于设置第一个 (的终点，在此示例中，仅将 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory) 结构的) 元素设置为草稿区域的结尾。 如果有多个堆，则终结点将设置为此堆的末尾，下一个堆将从该堆栈结束的位置开始。

 

