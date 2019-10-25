---
title: 线程同步和 TDR
description: 线程同步和 TDR
ms.assetid: 3690ad06-002a-4939-9b04-b87245678464
keywords:
- 线程 WDK 显示，TDR
- 同步 WDK 显示，TDR
- TDR （超时检测和恢复） WDK 显示和线程同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0898d70c34d915ca2096019e85ab655f649e59c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825502"
---
# <a name="thread-synchronization-and-tdr"></a>线程同步和 TDR


下图显示了在 Windows 显示驱动程序模型（WDDM）中，线程同步如何适用于显示微型端口驱动程序。

![阐释 windows vista 线程同步的关系图](images/lddmsync.png)

如果发生硬件超时，则将启动[超时检测和恢复（TDR）](timeout-detection-and-recovery.md)进程。 GPU 计划程序将调用驱动程序的[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)函数，该函数将重置 GPU。 *DxgkDdiResetFromTimeout*与任何其他显示微型端口驱动程序函数同步调用，而运行时电源管理功能[*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)和[*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)除外。 也就是说，当*DxgkDdiResetFromTimeout*线程运行时，驱动程序中不会运行任何其他线程。 操作系统还保证在调用*DxgkDdiResetFromTimeout*期间，不能从任何应用程序访问帧缓冲区。因此，驱动程序可以重置内存控制器阶段锁定循环（PLL）等。

当恢复线程执行[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)时，可以继续调用中断和延迟过程调用（dpc）。 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)函数可用于通过设备中断来同步重置过程的部分。

驱动程序从[*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)返回后，可以再次调用大多数驱动程序函数，操作系统会开始清理不再需要的资源。 在清理期间，出于以下原因，将调用以下驱动程序函数：

-   调用该驱动程序，通知即将逐出分配。

    例如，如果分配在内存段中分页，则会调用驱动程序的[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数，并将[**DXGKARG\_BUILDPAGINGBUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_buildpagingbuffer)结构的**操作**成员设置为 DXGK\_操作\_传输并将**传输. Size**成员设置为零，以通知驱动程序逐出。 请注意，不涉及任何内容传输，因为内容在重置过程中丢失。

    如果分配在口径段内分页，则使用 DXGKARG\_BUILDPAGINGBUFFER 设置为 DXGK\_操作的**操作**成员调用驱动程序的[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数，\_取消映射\_口径\_段，通知驱动程序从口径取消分配。

-   调用驱动程序的[*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)函数以释放 unswizzling 口径和分段口径范围。

除非绝对必要，否则驱动程序不能在前面的调用期间访问 GPU。

清除时间段结束后，操作系统将调用驱动程序的[*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)函数，以通知驱动程序清理已完成，并且操作系统将使用适配器进行呈现。

**请注意**  已为 Windows 8 更新 TDR 功能。 请参阅[Windows 8 中的 TDR 更改](tdr-changes-in-windows-8.md)。

 

 

 





