---
title: IddCx 对象
description: IddCx 使用可扩展 UMDF 对象模型来表示图形对象，以下各节中介绍。
ms.assetid: B4D40C6B-DCEF-4661-9DF2-411326870014
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67831ae640752456b51bf06d7a248632039dd571
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380195"
---
# <a name="iddcx-objects"></a>IddCx 对象


IddCx 使用可扩展 UMDF 对象模型来表示图形对象，以下各节中介绍。 UMDF 对象模型允许驱动程序特定存储要与每个 IddCx 相关联 (并因此 UMDF) 对象，详细信息，请参阅 UMDF 对象模型

## <a name="span-ididdcxadapterspanspan-ididdcxadapterspaniddcxadapter"></a><span id="IDDCX_ADAPTER"></span><span id="iddcx_adapter"></span>IDDCX\_适配器


此对象表示单个逻辑显示适配器创建的两阶段过程中的驱动程序。 首先，它将调用[ **IddCxAdapterInitAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nf-iddcx-iddcxadapterinitasync)回调函数和操作系统调用的驱动程序[EvtIddCxAdapterInitFinished](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nc-iddcx-evt_idd_cx_adapter_init_finished) DDI 无法完成初始化。

在简单的情况下，没有创建附加的间接显示设备的即插子系统的 UMDF 设备对象之间的一对一映射并**IDDCX\_适配器**驱动程序创建。 在单一间接显示硬件保护装置其中包含多个插设备 （例如 2 个 USB 设备函数） 更复杂的情况下，它是驱动程序创建只有一个的责任**IDDCX\_适配器**对象对于多个 UMDF 设备对象创建，另一个用于每个即插即用设备。 该驱动程序必须考虑以下方法在此方案中：

1. **IDDCX\_适配器**应仅创建后已成功启动构成间接显示解决方案的所有设备
2. 驱动程序必须向其传递一个**WDFDEVICE**时创建的适配器，因此它需要逻辑来决定它将通过哪个 UMDF 设备。
3. 如果有硬件错误任何构成间接显示适配器的设备，该驱动程序应报告组成为错误的适配器的所有设备。
间接显示模型不具有显式销毁适配器回调。 已成功完成适配器初始化序列后, 适配器有效，直到停止在初始化时传递的 UMDF 设备。 在创建适配器时，该驱动程序将提供有关间接显示适配器的静态适配器信息。

## <a name="span-ididdcxmonitorspanspan-ididdcxmonitorspaniddcxmonitor"></a><span id="IDDCX_MONITOR"></span><span id="iddcx_monitor"></span>IDDCX\_监视器


此对象表示特定监视器连接到间接显示适配器上的连接器之一。

该驱动程序在两阶段过程中创建监视对象。 首先，驱动程序调用[ **IddCxMonitorCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nf-iddcx-iddcxmonitorcreate)回调创建**IDDCX\_监视器**对象，然后调用[ **IddCxMonitorArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nf-iddcx-iddcxmonitorarrival)回调完成监视器到达。 当监视器被拔出，驱动程序将调用[ **IddCxMonitorDeparture** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iddcx/nf-iddcx-iddcxmonitordeparture)回调报告监视器已被拔出，这将导致**IDDCX\_监视器**要销毁对象。 即使相同的监视器是未插入又重新连接， **IddCxMonitorDeparture**/**IddCxMonitorArrival**序列需要再次调用。 **IDDCX\_监视器**的子**IDDCX\_适配器**对象。

## <a name="span-ididdcxswapchainspanspan-ididdcxswapchainspaniddcxswapchain"></a><span id="IDDCX_SWAPCHAIN"></span><span id="iddcx_swapchain"></span>IDDCX\_SWAPCHAIN


此对象表示将提供要在已连接监视器上显示的桌面映像 swapchain。 Swapchain 具有多个缓冲区，可允许 OS 在编写一个缓冲区中下一步的桌面映像，而间接显示器驱动程序正在访问的另一个缓冲区。 **IDDCX\_SWAPCHAIN**的子**IDDCX\_监视器**以便仅有一个分配的 swapchain 到给定监视器在任何时间。 操作系统创建和销毁**IDDCX\_SWAPCHAIN**对象，并分配/unassigns 它们对监视器使用的 EvtIddCxMonitorAssignSwapChain 和 EvtIddCxMonitorUnassignSwapChain Ddi 调用。

## <a name="span-ididdcxopmctxspanspan-ididdcxopmctxspaniddcxopmctx"></a><span id="IDDCX_OPMCTX"></span><span id="iddcx_opmctx"></span>IDDCX\_OPMCTX


此对象表示单个应用程序的应用程序可用于控制一台监视器上的输出保护 OPM 上下文从活动的 OPM 上下文。 多个 OPM 上下文可以在同一时间给定 monitor 上有效。 操作系统调用驱动程序来创建和销毁使用驱动程序的 EvtIddCxMonitorOPMCreateProtectedOutput OPM 上下文并 EvtIddCxMonitorOPMDestroyProtectedOutput DDI 调用。

 

 





