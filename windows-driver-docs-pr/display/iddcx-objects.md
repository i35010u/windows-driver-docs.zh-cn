---
title: IddCx 对象
description: IddCx 使用可扩展的 UMDF 对象模型来表示图形对象，以下各节将对这些对象进行介绍。
ms.assetid: B4D40C6B-DCEF-4661-9DF2-411326870014
ms.date: 07/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5ab7ebb0160be42da0a1020913a240c75cd7fbca
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459215"
---
# <a name="iddcx-objects"></a>IddCx 对象

[IddCx](/windows-hardware/drivers/ddi/iddcx/) （间接显示驱动程序类扩展）使用可扩展的 UMDF 对象模型来表示间接显示设备的组件。 [UMDF](/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)对象模型允许将特定于驱动程序的存储与每个 IddCx （因而是 UMDF）对象相关联。 有关详细信息，请参阅[UMDF 对象模型](/windows-hardware/drivers/wdf/umdf-objects-and-interfaces)。

创建 IDD 对象的顺序如下：

* 驱动程序首先创建一个**IDDCX_ADAPTER**对象。
* 然后，该驱动程序将创建一个**IDDCX_MONITOR**对象。
* 创建**IDDCX_ADAPTER**和**IDDCX_MONITOR**对象后，操作系统会创建**IDDCX_SWAPCHAIN**和**IDDCX_OPMCTX**对象，并将它们发送到驱动程序。

以下各节提供了有关这些对象的更多详细信息。

## <a name="iddcx_adapter"></a>IDDCX_ADAPTER

此对象表示由驱动程序在两阶段过程中创建的单个逻辑显示适配器：

* 驱动程序调用[**IddCxAdapterInitAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterinitasync)回调函数。
* OS 调用驱动程序的[*EvtIddCxAdapterInitFinished*](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_adapter_init_finished) DDI 来完成初始化。

IDD 模型没有显式销毁适配器回调。 成功完成适配器初始化序列后，适配器将有效，直到在初始化时传递的 UMDF 设备停止。 创建适配器时，驱动程序提供有关间接显示适配器的静态适配器信息。

### <a name="handling-multifunction-devices"></a>处理多功能设备

最简单的情况是，附加的间接显示设备的即插即用子系统创建的 UMDF 设备对象与间接显示驱动程序（IDD）创建的**IDDCX_ADAPTER**对象之间有一对一的映射。

可以有更复杂的方案，其中单个间接显示连接器包含多个即插即用设备。 例如，间接显示解决方案可能有多个 PnP 设备功能，如麦克风（音频驱动程序）和照相机（视频驱动程序）。 在这种情况下，IDD 负责为每个 PnP 设备创建的多个 UMDF 设备对象创建一个**IDDCX_ADAPTER**对象。 在此方案中，驱动程序需要考虑以下事项：

* 仅当所有组成间接显示解决方案的 PnP 设备已成功启动后，才应创建**IDDCX_ADAPTER** 。
* 创建适配器时，驱动程序必须传递单个**WDFDEVICE** ，因此需要使用逻辑来确定它将通过哪个 UMDF 设备。
* 如果组成间接显示适配器的任何设备都出现硬件错误，则驱动程序应报告使适配器出现错误的所有设备。

## <a name="iddcx_monitor"></a>IDDCX_MONITOR

此对象表示连接到间接显示适配器上某个连接器的特定监视器。

驱动程序在两阶段过程中创建 monitor 对象：

* 它首先调用[**IddCxMonitorCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorcreate)回调来创建**IDDCX_MONITOR**对象。
* 然后，它调用[**IddCxMonitorArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorarrival)回调来完成监视器到达。

当拔出监视器时，驱动程序将调用[**IddCxMonitorDeparture**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitordeparture)回调来报告监视器已拔出，这会导致**IDDCX_MONITOR**的对象被销毁。 即使已重新连接同一监视器，也**IddCxMonitorDeparture** / 需再次调用 IddCxMonitorDeparture**IddCxMonitorArrival**序列。

**IDDCX_MONITOR**是**IDDCX_ADAPTER**对象的子对象。

## <a name="iddcx_swapchain"></a>IDDCX_SWAPCHAIN

此对象表示一个[存在](https://docs.microsoft.com/windows/win32/direct3d12/swap-chains)，该对象将提供要在连接的监视器上显示的桌面映像。 存在有多个缓冲区，可让 OS 在一个缓冲区中组合下一个桌面映像，同时 IDD 会访问另一个缓冲区。 **IDDCX_SWAPCHAIN**是**IDDCX_MONITOR**的子级，因此，在任何时候都只有一个分配给给定监视器的存在。

OS 创建并销毁**IDDCX_SWAPCHAIN**对象，并使用[**EvtIddCxMonitorAssignSwapChain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_assign_swapchain)和[**EvtIddCxMonitorUnassignSwapChain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_unassign_swapchain) Ddi 调用将它们分配/其分配到监视器。

## <a name="iddcx_opmctx"></a>IDDCX_OPMCTX

此对象表示来自单个应用程序 OPM 上下文的活动[输出保护管理器](https://docs.microsoft.com/windows/win32/medfound/output-protection-manager)（OPM）上下文，应用程序可使用该上下文控制单个监视器上的输出保护。 给定监视器上的多个 OPM 上下文可以同时处于活动状态。 操作系统使用驱动程序的[**EvtIddCxMonitorOPMCreateProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_opm_create_protected_output)和[**EvtIddCxMonitorOPMDestroyProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_opm_destroy_protected_output) DDI 调用来调用驱动程序来创建和销毁 OPM 上下文。
