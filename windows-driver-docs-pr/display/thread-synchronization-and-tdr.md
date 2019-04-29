---
title: 线程同步和 TDR
description: 线程同步和 TDR
ms.assetid: 3690ad06-002a-4939-9b04-b87245678464
keywords:
- 线程处理 WDK 显示，TDR
- 同步 WDK 显示，TDR
- （超时检测和恢复） TDR WDK 显示和线程同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eb751975e830909465d5a22086ba31f21d1d878
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389867"
---
# <a name="thread-synchronization-and-tdr"></a>线程同步和 TDR


下图显示了线程同步显示微型端口驱动程序在 Windows 显示驱动程序模型 (WDDM) 的工作原理。

![说明 windows vista 的线程同步的关系图](images/lddmsync.png)

如果发生硬件超时，请[超时检测和恢复 (TDR)](timeout-detection-and-recovery.md)处理启动。 GPU 计划程序调用的驱动程序[ *DxgkDdiResetFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559815)函数，这会重置 GPU。 *DxgkDdiResetFromTimeout*称为以同步方式与任何其他显示微型端口驱动程序函数，但运行时的电源管理功能除外[ *DxgkDdiSetPowerComponentFState* ](https://msdn.microsoft.com/library/windows/hardware/hh451422)并[ *DxgkDdiPowerRuntimeControlRequest*](https://msdn.microsoft.com/library/windows/hardware/hh451396)。 没有其他线程中驱动程序时运行的即*DxgkDdiResetFromTimeout*线程运行。 操作系统还可确保从任何应用程序在调用期间，不能访问帧缓冲区则会出现*DxgkDdiResetFromTimeout*; 因此，驱动程序等可重置内存控制器阶段锁定的循环 (PLL)。

恢复线程执行的同时[ *DxgkDdiResetFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559815)、 中断和延迟过程调用 (Dpc) 可以继续进行调用。 [ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)函数可用于与设备中断同步重置过程的部分。

从驱动程序返回后[ *DxgkDdiResetFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559815)，可以再次调用大多数驱动程序函数，并在操作系统启动清理不再需要的资源。 在清理期间，以下驱动程序函数将调用所指示的原因：

-   该驱动程序调用以通知有关分配，正在退出。

    例如，如果分配已分页的内存段，在驱动程序[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)使用调用函数**操作**的成员[**DXGKARG\_BUILDPAGINGBUFFER** ](https://msdn.microsoft.com/library/windows/hardware/ff557540)结构设置为 DXGK\_操作\_传输和与**Transfer.Size**成员设置为零，通知驱动程序出现了逐出。 请注意，没有内容传输所涉及因为内容在重置期间丢失。

    如果分配了分页中 aperture 分段，驱动程序的[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)使用调用函数**操作**DXGKARG成员\_BUILDPAGINGBUFFER 设置为 DXGK\_操作\_UNMAP\_APERTURE\_段以告知取消映射的分配额 aperture 的驱动程序。

-   在驱动程序[ *DxgkDdiReleaseSwizzlingRange* ](https://msdn.microsoft.com/library/windows/hardware/ff559786)调用函数以释放取消调配 aperture 和段 aperture 范围。

该驱动程序不应访问 GPU 在前面过程调用除非绝对必要。

清理期限结束后，操作系统将调用的驱动程序[ *DxgkDdiRestartFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559820)函数来通知该驱动程序的清除已完成，并且将恢复操作系统用于呈现使用适配器。

**请注意**  TDR 功能已更新为 Windows 8。 请参阅[TDR 更改在 Windows 8 中的](tdr-changes-in-windows-8.md)。

 

 

 





