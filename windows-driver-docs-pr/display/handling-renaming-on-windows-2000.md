---
title: 在 Windows 2000 上处理重命名
description: 在 Windows 2000 上处理重命名
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、顶点缓冲区、在 Windows 上重命名2000
- 顶点缓冲 WDK DirectX 8.0，在 Windows 2000 上重命名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7567c5c5c8a3c1a3b259ac70d7616f6f58a612fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819579"
---
# <a name="handling-renaming-on-windows-2000"></a>在 Windows 2000 上处理重命名


## <span id="ddk_handling_renaming_on_windows_2000_gg"></span><span id="DDK_HANDLING_RENAMING_ON_WINDOWS_2000_GG"></span>


为了正确执行顶点缓冲区重命名，必须了解在 Windows 2000 和更高版本上的 **fpVidMem** 指针存储在 surface global 对象中的特性。 **FpVidMem** 的解释取决于存储图面的内存类型。 对于 "系统" 和 "非本地" 视频内存 (AGP) 图面上， **fpVidMem** 是直接指向拥有该表面的进程的用户模式地址空间的指针。

对于本地视频内存表面， **fpVidMem** 是从视频内存开始的偏移量。 若要将此转换为用户模式指针，需要添加映射到用户模式进程的视频内存基址。 可在给定进程的 DirectDraw 本地对象的 **fpProcess** 字段中找到此基址。

尽管非本地视频内存表面的 **fpVidMem** 只是用户模式指针，但生成此用户模式指针的方式有些复杂。 需要了解 Windows 2000 内核如何维护 AGP 堆并管理它们的图面分配。 第一个要点是，对于非本地堆，由内核维护的堆的起始地址不能为任何实际地址空间的堆。 事实上，这通常是一个数字偏移，旨在确保来自该堆的有效分配不能具有 **NULL** (零) 地址。

将 AGP 堆视为不与任何实际地址空间对应的概念地址空间可能会很有帮助。 AGP 堆的 **fpStart** 字段是此概念地址空间中堆的基址。 此外，从 AGP 堆中分配的任何表面都具有 **fpHeapOffset** ，此概念地址空间也是如此。 因此， **fpHeapOffset** 是与此概念堆的基的偏移量，并且它不是相对于堆本身开头的偏移量。 此外，它不是指向任何实际地址空间的指针。 为了使用户模式进程能够访问 surface **fpHeapOffset** 的内存，必须通过指针算法将)  (映射到该用户模式进程的地址空间。 创建图面时，内核会根据下面概述的公式执行此映射。

给定一个 surface (**pSurface**) ，一个内核模式 AGP 堆 (**pvmHeap**) 并将堆映射到特定的用户模式进程 (**pMap**) ，以下公式用于计算表面的实际用户模式 **fpVidMem** ：

```cpp
fpVidMem = pMap->pvVirtAddr +
    (pSurface->fpHeapOffset âˆ’ pvmHeap->fpStart)
```

**pvVirtAddr** 是 AGP 堆到给定进程的用户模式映射的基址。 **fpStart** 是 AGP 堆的基的偏移量到前面所述的概念地址空间中，而 **fpHeapOffset** 是从同一概念地址空间的基开始的图面的偏移量。

你的驱动程序将通过 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 回调通知 AGP 堆的概念基址。 当用 GUID UpdateNonLocalHeap 调用 *DdGetDriverInfo* 时 \_ ，传递的数据结构的 **fpGARTLin** 字段的值与 **fpStart** 的值相同，即概念地址空间中 AGP 堆开头的基址。 遗憾的是，您的驱动程序不会收到 **pvVirtAddr** 的值通知，并且通过传递到该驱动程序的任何数据结构对该驱动程序都不可见。 因此，它的值必须从内核针对顶点缓冲区计算的 **fpVidMem** 计算。 给定内核计算的 **fpVidMem** ，只需将当前 **fpHeapOffset** 减去堆的 **fpStart**。 如果在重命名时将新内存的 **fpHeapOffset** 交换到顶点缓冲区中，则可以轻松计算 **fpVidMem** 的新值。

下面的代码段演示了如何在锁定调用中为 AGP 表面计算新 **fpVidMem** 。

```cpp
// Get the vertex buffer's surface local and global from the
// lock data
LPDDRAWI_DDRAWSURFACE_LCL*pLcl = pLockData->lpDDSurface;
LPDDRAWI_DDRAWSURFACE_GBL*pGbl = pLcl->lpGbl;

// Get heap this vertex buffer was allocated from
LPVVIDEOMEMORY pHeap = pGbl->lpVidMemHeap;

// Get the current fpVidMem for the vertex buffer
FLATPTR fpCurrentVidMem = pGbl->fpVidMem;

// Compute the virtual base address of the mapping of this AGP
// into the process owning this vertex buffer.
FLATPTR pvVirtAddr = fpCurrentVidMem âˆ’
                     (pGbl->fpHeapOffset âˆ’ pHeap->fpStart);

// Given the fpHeapOffset of the nonlocal video memory to be
// swapped into the new vertex buffer compute the new fpVidMem
// as follow
FLATPTR fpNewVidMem = pvVirtAddr + (fpNewHeapOffset âˆ’ pHeap->fpStart);

// Now store the new fpVidMem in the surface global object and
// also in the lock data.
pGbl->fpHeapOffset = fpNewHeapOffset;
pGbl->fpVidMem = fpNewVidMem;
pLockData->lpSurfData = fpNewVidMem;

// Return success and driver handled
pLockData->ddRVal = DD_OK;
return DDHAL_DRIVER_HANDLED;
```

为了使非本地视频内存可用于用户模式进程，需要将内存提交并映射到用户模式进程。 若要确保在执行顶点缓冲区重命名时执行此操作，这一点很重要，使用 **Eng**_Xxx_ 函数 [**HeapVidMemAllocAligned**](/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)分配顶点缓冲区的新内存。 这可以确保在使用之前提交和映射内存。 **HeapVidMemAllocAligned** 返回 AGP 堆的概念地址空间的偏移量，因此，此指针可直接用作 **fpHeapOffset** 。

如果驱动程序返回 DDHAL \_ 驱动程序，而该驱动程序 \_ 已处理 AGP 图面的锁定，则内核代码将在 [**DD \_ LOCKDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_lockdata)数据结构中将 **lpSurfData** 的值返回到运行时和应用程序。 如果驱动程序返回 DDHAL \_ 驱动程序 \_ NOTHANDLED，内核只是将 **fpVidMem** 的值返回到用户模式。 因此， \_ \_ 只要将 **fpVidMem** 更新为指向新的用户模式指针，就不必返回已处理的 DDHAL 驱动程序。 但是，我们建议驱动程序将设置为 **fpVidMem** 和 **LPSURFDATA** 并返回 DDHAL \_ 驱动程序已 \_ 处理。

 

