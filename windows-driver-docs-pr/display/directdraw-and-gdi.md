---
title: DirectDraw 和 GDI
description: DirectDraw 和 GDI
keywords:
- 显示驱动程序 WDK Windows 2000，DirectDraw
- DirectDraw WDK Windows 2000 显示，GDI
- GDI DirectDraw 支持 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，图形
- 图形 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e28c93ea561cbf3b39555e919d1e6f70bbd0e2e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809403"
---
# <a name="directdraw-and-gdi"></a>DirectDraw 和 GDI


## <span id="ddk_directdraw_and_gdi_gg"></span><span id="DDK_DIRECTDRAW_AND_GDI_GG"></span>


当初始化显示驱动程序时，GDI 会自动启用 DirectDraw。 若要在 DirectDraw 与驱动程序的图形 DDI 部分之间提供更好的交互，还支持 DirectDraw DDI 的驱动程序可以实现或调用以下函数：

<span id="DrvDeriveSurface"></span><span id="drvderivesurface"></span><span id="DRVDERIVESURFACE"></span>[**DrvDeriveSurface**](/windows/win32/api/winddi/nf-winddi-drvderivesurface)  
驱动程序实现的函数，该函数可在 DirectDraw 驱动程序图面周围包装 GDI 驱动程序图面，从而使任何 GDI 绘图能够更快地进行硬件加速 (而不是通过 *DIB* 引擎) 在软件中进行绘制。 通常情况下，如果驱动程序已支持屏幕外设备位图，则此函数应仅要求额外的几行代码。

[**DrvDeriveSurface**](/windows/win32/api/winddi/nf-winddi-drvderivesurface) 改善了也使用 GDI 的 DirectDraw 应用程序的性能，并且它还消除了将软件游标与 DirectDraw 或 Direct3D 应用程序一起使用时的游标闪烁。

<span id="HeapVidMemAllocAligned_and_VidMemFree"></span><span id="heapvidmemallocaligned_and_vidmemfree"></span><span id="HEAPVIDMEMALLOCALIGNED_AND_VIDMEMFREE"></span>[**HeapVidMemAllocAligned**](/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)和 [ **VidMemFree**](/windows/win32/api/dmemmgr/nf-dmemmgr-vidmemfree)  

驱动程序调用的函数，它使用 DirectDraw *堆管理器* 进行所有 [*非屏幕内存*](video-present-network-terminology.md#off_screen_memory) 管理。 [**DrvCreateDeviceBitmap**](/windows/win32/api/winddi/nf-winddi-drvcreatedevicebitmap) 应调用 [**HeapVidMemAllocAligned**](/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned) 来请求 DirectDraw 为 GDI 位图分配空间; [**DrvDeleteDeviceBitmap**](/windows/win32/api/winddi/nf-winddi-drvdeletedevicebitmap) 应调用 [**VidMemFree**](/windows/win32/api/dmemmgr/nf-dmemmgr-vidmemfree) 来释放此分配。

DirectDraw 的优先级高于驱动程序的图形 DDI 部分以实现屏幕上的内存分配。 驱动程序应与 DirectDraw [*DdFreeDriverMemory*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_freedrivermemory) 回调挂钩，这允许驱动程序从屏幕内存中删除 GDI 面，以便为更高优先级的 DirectDraw 表面分配腾出空间。

[**HeapVidMemAllocAligned**](/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)和 [**VidMemFree**](/windows/win32/api/dmemmgr/nf-dmemmgr-vidmemfree)都在 *dmemmgr* 中声明，后者随 Windows 驱动程序工具包一起提供 (WDK) 。 在 \_ \_ \_ \_ 包含此标头文件之前，驱动程序可能必须定义 NTDDKCOMP。

 

