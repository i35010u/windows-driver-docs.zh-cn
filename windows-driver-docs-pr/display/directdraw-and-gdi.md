---
title: DirectDraw 和 GDI
description: DirectDraw 和 GDI
ms.assetid: 22106821-dac1-4c99-bf2c-c051b5a8893a
keywords:
- 显示驱动程序 WDK Windows 2000，DirectDraw
- DirectDraw WDK Windows 2000 显示 GDI
- GDI DirectDraw 支持 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000 中，图形
- 显示图形 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c358d551fc7f383bb7e0d3676a1ff956c913364f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390495"
---
# <a name="directdraw-and-gdi"></a>DirectDraw 和 GDI


## <span id="ddk_directdraw_and_gdi_gg"></span><span id="DDK_DIRECTDRAW_AND_GDI_GG"></span>


GDI 显示驱动程序初始化时，会自动启用 DirectDraw。 若要提供更好 DirectDraw 和驱动程序的图形 DDI 部分之间的交互，还支持 DirectDraw DDI 的驱动程序可以实现或调用以下函数：

<span id="DrvDeriveSurface"></span><span id="drvderivesurface"></span><span id="DRVDERIVESURFACE"></span>[**DrvDeriveSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556188)  
包装 DirectDraw 驱动程序面周围的 GDI 驱动程序表面的驱动程序实现的函数，允许任何 GDI 绘制到 DirectDraw 视频内存或 AGP 图面是硬件加速 (而不是通过软件中绘制*DIB*引擎)。 通常情况下，如果该驱动程序已支持设备屏幕外位图，此函数应要求只有几行额外的代码。

[**DrvDeriveSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556188)提高 DirectDraw 应用程序，还使用 GDI，和它也消除了光标闪烁 DirectDraw 或 Direct3D 应用程序中使用软件游标时的性能。

<span id="HeapVidMemAllocAligned_and_VidMemFree"></span><span id="heapvidmemallocaligned_and_vidmemfree"></span><span id="HEAPVIDMEMALLOCALIGNED_AND_VIDMEMFREE"></span>[**HeapVidMemAllocAligned** ](https://msdn.microsoft.com/library/windows/hardware/ff567267)并[ **VidMemFree**](https://msdn.microsoft.com/library/windows/hardware/ff570554)  

驱动程序调用的函数的使用 DirectDraw*堆管理器*所有[*屏幕外内存*](video-present-network-terminology.md#off_screen_memory)管理。 [**DrvCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556185)应调用[ **HeapVidMemAllocAligned** ](https://msdn.microsoft.com/library/windows/hardware/ff567267)请求 DirectDraw 为 GDI 位图; 分配空间[ **DrvDeleteDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556187)应调用[ **VidMemFree** ](https://msdn.microsoft.com/library/windows/hardware/ff570554)来释放此分配。

DirectDraw 优先于屏幕外内存分配的驱动程序的图形 DDI 部分。 该驱动程序应将挂钩 DirectDraw [ *DdFreeDriverMemory* ](https://msdn.microsoft.com/library/windows/hardware/ff549360)回调，它将允许驱动程序从屏幕外内存，以便为更高优先级 DirectDraw 面让出空间删除 GDI 图面分配。

这两[ **HeapVidMemAllocAligned** ](https://msdn.microsoft.com/library/windows/hardware/ff567267)并[ **VidMemFree** ](https://msdn.microsoft.com/library/windows/hardware/ff570554)中声明*dmemmgr.h*、 哪些提供使用 Windows Driver Kit (WDK)。 驱动程序可能需要定义\_ \_NTDDKCOMP\_ \_之前包括此标头文件。

 

 





