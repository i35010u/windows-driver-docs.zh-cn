---
title: 回调处理的非本地显示内存图面
description: 回调处理的非本地显示内存图面
ms.assetid: 803c52df-93c4-4124-9e17-6ef6c734a15f
keywords:
- 显示内存 WDK DirectDraw，回调
- 非本地显示内存 WDK DirectDraw，回调
- AGP WDK DirectDraw 回调
- 绘制 AGP 支持 WDK DirectDraw，回调
- DirectDraw AGP 支持 WDK Windows 2000 显示中，回调
- 内存 WDK DirectDraw AGP，回调
- 回调 WDK DirectDraw 非本地内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 714e3e4795a97f342eb69229951fb82e3805bf46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540756"
---
# <a name="callback-handling-of-nonlocal-display-memory-surfaces"></a>回调处理的非本地显示内存图面


## <span id="ddk_callback_handling_of_nonlocal_display_memory_surfaces_gg"></span><span id="DDK_CALLBACK_HANDLING_OF_NONLOCAL_DISPLAY_MEMORY_SURFACES_GG"></span>


非本地显示内存图面将被视为在本地显示在驱动程序回调方面的内存图面作为完全相同的方式。 例如，驱动程序的[ *DdCanCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549213)尝试创建非本地 （以及本地） 显示内存表面时调用回调[ *DdBlt*](https://msdn.microsoft.com/library/windows/hardware/ff549205)时，将调用本地副本和非本地之间的平面闪显示内存图面，并[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)被放弃的图面上的内存时，将调用。

使用相同的驱动程序功能来进行这两个本地和非本地显示内存图面，因为驱动程序必须显示检查传入的应用层的内存类型。 可以通过检查来确定内存类型**ddsCaps.dwCaps**图面上的本地对象的成员[ **DD\_图面\_本地**](https://msdn.microsoft.com/library/windows/hardware/ff551733)传递向针对功能驱动程序的位将 DDSCAPS\_LOCALVIDMEM 和 DDSCAPS\_NONLOCALVIDMEM。

应用程序和 AGP 硬件访问使用两个不同的地址的 DirectDraw 表面的位。 应用程序使用通过操作系统的物理地址空间部分的页表转换的虚拟地址。 此物理地址空间由用于似乎是连续的 GART 硬件映射。 硬件访问此物理的线性地址 （再次重新映射到实际的不连续的内存页通过 GART）。 **FpVidMem**的成员[ **DD\_图面\_全局**](https://msdn.microsoft.com/library/windows/hardware/ff551726)结构保存的虚拟的线性地址对应用程序有用 （和有可能某些驱动程序操作）。 可从设备端物理地址：

```cpp
fpStartOffset = pSurface->fpHeapOffset - pSurface->lpVidMemHeap->fpStart;
```

随后将此偏移量添加到设备的 GART 物理基址 (包含在**liPhysAGPBase**的成员[ **VMEMHEAP** ](https://msdn.microsoft.com/library/windows/hardware/ff570561)结构)。

在所有其他方面，非本地显示内存曲面的行为完全像本地显示内存图面一样。 应用程序尝试访问非本地显示内存曲面的图面上的数据时，驱动程序将接收锁请求。 如 blts 非本地之间的操作显示内存和本地显示内存可以是异步的就像它们可在本地显示内存图面之间。 尝试锁定非本地显示内存图面时涉及这些图面操作仍是挂起的应故障的驱动程序和 DDERR\_WASSTILLDRAWING 按常规方式的错误代码。

此外，尽管 DirectDraw 管理分配和释放的非本地显示代表该驱动程序的内存图面，该驱动程序的创建和销毁的非本地显示内存中的图面，仍会通知。 当销毁非本地显示内存图面时，该驱动程序不应返回直到面不再使用。

非本地显示内存[丢失](losing-and-restoring-directdraw-surfaces.md)中完全相同的方式为本地显示内存，也就是说，模式切换时或排他模式更改时，显示本地和非本地内存的所有曲面都都将丢失和[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)驱动程序回调调用为每个面。 但是，DirectDraw 不保证保留实际的保留的地址范围和提交的内存。 DirectDraw 可以选择放弃所有已提交的内存和保留的地址范围，或者它可能会选择解除内存但保留地址范围。 它可能还会保留两者，并只是将标记为已丢失的图面。 驱动程序不应进行这些方案中的任何一个上基于的假设。

 

 





