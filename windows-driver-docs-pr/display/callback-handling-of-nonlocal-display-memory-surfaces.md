---
title: 非本地显示内存图面的回调处理
description: 非本地显示内存图面的回调处理
ms.assetid: 803c52df-93c4-4124-9e17-6ef6c734a15f
keywords:
- 显示内存 WDK DirectDraw，回调
- 非本地显示内存 WDK DirectDraw，回调
- AGP WDK DirectDraw，回调
- 绘制 AGP 支持 WDK DirectDraw，回调
- DirectDraw AGP 支持 WDK Windows 2000 显示，回调
- 内存 WDK DirectDraw AGP，回调
- 回拨 WDK DirectDraw 非本地内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f8081abc76a30a12e98fc849b5ce8c20df23b51
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423918"
---
# <a name="callback-handling-of-nonlocal-display-memory-surfaces"></a>非本地显示内存图面的回调处理


## <span id="ddk_callback_handling_of_nonlocal_display_memory_surfaces_gg"></span><span id="DDK_CALLBACK_HANDLING_OF_NONLOCAL_DISPLAY_MEMORY_SURFACES_GG"></span>


非本地显示内存图面的处理方式与驱动程序回调中的本地显示内存表面完全相同。 例如，当尝试创建非本地 (以及本地) 显示内存图面时，将调用驱动程序的 [*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85)) 回调，当在本地和非本地显示内存图面之间 blitting 时，将调用 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) ，而当表面内存被丢弃时调用 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 。

由于相同的驱动程序函数同时用于本地和非本地显示内存图面，因此驱动程序必须显式检查传入图面的内存类型。 可以通过检查 **ddsCaps** 的本地 Surface 对象 [**DD \_ \_ surface**](/windows/win32/api/ddrawint/ns-ddrawint-dd_surface_local) DdsCaps \_ LOCALVIDMEM 和 ddsCaps NONLOCALVIDMEM 的 dwCaps 成员，来确定内存类型 \_ 。

应用程序和 AGP 硬件使用两个不同的地址访问 DirectDraw 表面的位。 应用程序使用通过操作系统的页表转换为物理地址空间部分的虚拟地址。 此物理地址空间由 GART 硬件映射以便显示连续。 硬件通过 GART) 将此物理线性地址 (重新映射到实际的不连续的内存页。 [**DD \_ SURFACE \_ 全局**](/windows/win32/api/ddrawint/ns-ddrawint-dd_surface_global)结构的**fpVidMem**成员保存了虚拟线性地址，这对应用程序 (，并可能) 一些驱动程序操作。 可从以下位置找到设备端物理地址：

```cpp
fpStartOffset = pSurface->fpHeapOffset - pSurface->lpVidMemHeap->fpStart;
```

然后，此偏移量将添加到设备的 GART 物理基址 (包含在[**VMEMHEAP**](/windows/win32/api/dmemmgr/ns-dmemmgr-vmemheap)结构) 的**liPhysAGPBase**成员中。

在所有其他方面，非本地显示内存表面的行为与本地显示内存表面完全相同。 当应用程序尝试访问非本地显示内存图面的表面数据时，驱动程序将收到锁请求。 非本地显示内存和本地显示内存之间的操作（如 blts）可以是异步操作，就像它们可以在本地显示内存图面之间一样。 当包含这些表面的操作仍处于挂起状态时，如果驱动程序的 DDERR WASSTILLDRAWING 错误代码仍处于挂起状态，则尝试锁定非本地显示内存图面 \_ 。

此外，尽管 DirectDraw 会代表驱动程序管理非本地显示内存表面的分配和释放，但仍会通知驱动程序在非本地显示内存中创建和销毁表面。 销毁非本地显示内存图面时，驱动程序不应返回，直到不再使用该表面。

非本地显示内存以与本地显示内存完全相同的方式 [丢失](losing-and-restoring-directdraw-surfaces.md) ，也就是说，当模式切换发生时或独占模式发生变化时，所有本地和非本地显示内存表面都将丢失，并且将为每个图面调用 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 驱动程序回调。 但是，DirectDraw 不保证保留的实际保留地址范围和提交的内存被保留。 DirectDraw 可以选择丢弃所有提交的内存和保留的地址范围，也可以选择解除内存，但保留地址范围。 它还可以保留并只是将曲面标记为丢失。 驱动程序不应根据这些方案中的任何一种来做出假设。

 

