---
title: 线性内存分配
description: 线性内存分配
ms.assetid: f39c6752-c771-43d4-b89e-77f3d542d1fd
keywords:
- 线性内存分配 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b6632a5c20124b7db1f08b0333bdd77bf20c85a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524697"
---
# <a name="linear-memory-allocation"></a>线性内存分配


## <span id="ddk_linear_memory_allocation_gg"></span><span id="DDK_LINEAR_MEMORY_ALLOCATION_GG"></span>


显示将内存视为*线性*每当，音调就可以更改以匹配的图面上的宽度，考虑到帐户对齐需求 （如在下图中所示）。 例如，如果 blitter 才命中 8 字节进步，并使用 31 像素子画面，需要进行调整以便对齐 8 字节边界上的下一行显示每个行。

像素深度，以字节为单位，乘以图面上的宽度，考虑到帐户的对齐要求取决于间距。 如果显示，跨 640 8 位像素，音调就为 640。 如果像素都是 16 位 （2 个字节） 并且 640 X 480 的屏幕中，则俯仰是 1280年 (640 \* 2)。 同样，640 宽、 32 位 （4 字节） 像素屏幕也有 2560年音调 (640 \* 4) 在线性显示内存中。

下图说明了具有一个主外围和一个暂存区域线性内存堆分配。

![说明线性内存堆分配的关系图](images/ddfig4.png)

指向主表面开头的指针是**fpPrimary**，属于[ **VIDEOMEMORYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff570172)结构。 通过指示主表面和各种 Windows 缓存添加到此提供的暂存区域中，开头的指针的大小**fpStart**的成员[ **VIDEOMEMORY**](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构。 终结点，由**fpEnd**的成员**VIDEOMEMORY**结构，请通过添加减一的剩余内存的大小计算。

[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构保存管理显示内存堆的信息。 此示例中的数组具有只有一个元素**VIDEOMEMORY**因为只有一个堆结构。 VIDMEM\_ISLINEAR 中的标志**dwFlags**的成员**VIDEOMEMORY**结构，这表示为线性的内存。

下面的伪代码演示如何[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构为线性内存设置：

```cpp
/*
 * video memory pool usage
 */
static VIDEOMEMORY vidMem [] = {
    { VIDMEM_ISLINEAR, 0x00000000, 0x00000000,
           { 0 }, { 0 } },
};/*
```

下面的伪代码显示了如何线性内存堆设置：

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

通过将 GDI 主表面的开头添加到主表面的大小和 Windows 画笔、 笔和 VDD 缓存的大小来计算的第一个可用的暂存区域开始。 使用结果的第一个元素中设置的起始点[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)到暂存区域的开始处的结构。

通过将暂存区域的开头添加到暂存区域的大小和减去一个以使其包含找到的暂存区域的末尾。 使用结果时要设置的终结点的第一个 （且，在此情况下，仅） 元素[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)到末尾的暂存区域的结构。 如果有多个堆，终结点设置为此堆和下一步堆结束这个后开始启动。

 

 





