---
title: 在 Windows 2000 上处理重命名
description: 在 Windows 2000 上处理重命名
ms.assetid: d8f533f8-3037-47c0-986b-bd283bb3804d
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，请在 Windows 2000 上重命名的顶点缓冲区
- 顶点缓冲区 WDK DirectX 8.0，Windows 2000 上重命名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9ad02e4dc44bef6deaf4a8de91e429fa7855bff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369861"
---
# <a name="handling-renaming-on-windows-2000"></a>在 Windows 2000 上处理重命名


## <span id="ddk_handling_renaming_on_windows_2000_gg"></span><span id="DDK_HANDLING_RENAMING_ON_WINDOWS_2000_GG"></span>


若要正确执行顶点缓冲区重命名它是必须了解的性质**fpVidMem** Windows 2000 及更高版本图面上的全局对象中存储的指针。 解释**fpVidMem**取决于内存中用于存储在图面类型。 对于系统和非本地视频内存 (AGP) 图面**fpVidMem**直接到拥有该图面进程的用户模式地址空间的指针。

对于本地的视频内存图面**fpVidMem**是从视频内存开头的偏移量。 为了将其转换为一个指针，用户模式下有必要添加视频内存的基址，如映射到用户模式进程。 可在此基址**fpProcess**给定进程的 DirectDraw 本地对象的字段。

尽管**fpVidMem**非本地的视频内存面是只是一个用户模式下指针都有点复杂，它可以生成此用户模式下指针的方法。 必须先了解如何在 Windows 2000 内核保持 AGP 堆和管理来自其图面上分配它。 第一个重要的一点是，对于非本地堆，堆维护由内核的起始地址可能不是堆到任何真实的地址空间。 它实际上是，通常情况下，设计为确保不能具有有效的堆中分配的数字的偏移量**NULL** （零） 地址。

它可能有助于将 AGP 堆视为驻留在不到任何真实的地址空间对应的概念的地址空间中。 **FpStart** AGP 堆的字段是此概念的地址空间中的堆的基址。 此外，还必须从 AGP 堆中分配任何图面**fpHeapOffset** ，还存在于此概念的地址空间中。 因此， **fpHeapOffset**此概念堆的基的偏移量，它是未从堆本身的开始的偏移量。 此外，不到任何真实的地址空间的指针。 为了使用户模式进程，若要访问的内存中的一个面**fpHeapOffset**必须 （通过指针算法） 映射到该用户模式进程的地址空间。 创建图面时，内核执行此映射依据的公式如下所述。

给定一个面 (**pSurface**)，内核模式 AGP 堆 (**pvmHeap**) 和堆的映射到特定的用户模式进程 (**pMap**)，下面的公式是用于计算实际，用户模式**fpVidMem**面的：

```cpp
fpVidMem = pMap->pvVirtAddr +
    (pSurface->fpHeapOffset âˆ’ pvmHeap->fpStart)
```

**pvVirtAddr**是的 AGP 堆用户模式下映射到给定进程的基址。 **fpStart**是的 AGP 堆到上面所述的概念的地址空间的基的偏移量和**fpHeapOffset**是相同的概念的地址空间从基面开头的偏移量。

您的驱动程序通知的 AGP 概念的基址的堆通过[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)回调。 当*DdGetDriverInfo*调用时所使用的 GUID\_UpdateNonLocalHeap **fpGARTLin**字段传递的数据结构是相同的值**fpStart**，它是的 AGP 开头的基址堆的概念的地址空间中。 遗憾的是，您的驱动程序不会通知的值的**pvVirtAddr**且不通过任何传递给驱动程序的数据结构的驱动程序对可见。 因此，其值必须计算得出**fpVidMem**计算的初始创建顶点缓冲区内核。 给定**fpVidMem**计算内核，只需减去当前**fpHeapOffset**更少的堆**fpStart**。 给定**fpHeapOffset**的新的内存来切换到上重命名的新值的顶点缓冲区**fpVidMem**可以轻松地计算。

下面的代码段演示如何计算的新**fpVidMem** AGP 面的锁调用中。

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

为使非本地的视频内存访问的用户模式进程，它是必需的要进行同时提交和映射到用户模式进程的内存。 若要确保这执行顶点缓冲区重命名时进行很重要，顶点缓冲区的新内存分配给使用 **Eng * * * Xxx*函数[ **HeapVidMemAllocAligned**](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned). 这可确保提交和使用之前映射内存。 **HeapVidMemAllocAligned**返回的偏移量的 AGP 堆，因此，此指针的概念的地址空间可用作**fpHeapOffset**直接。

如果该驱动程序返回 DDHAL\_驱动程序\_处理的锁是的 AGP 表面内核代码返回的值为**lpSurfData**中[ **DD\_LOCKDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_lockdata)到运行时和应用程序的数据结构。 如果该驱动程序返回 DDHAL\_驱动程序\_NOTHANDLED 内核只返回的值**fpVidMem**为用户模式。 因此，不需要返回 DDHAL\_驱动程序\_HANDLED 长达**fpVidMem**更新为指向新的用户模式下指针。 但是，我们建议，二者都设置为该驱动程序**fpVidMem**并**lpSurfData**并返回 DDHAL\_驱动程序\_已处理。

 

 





