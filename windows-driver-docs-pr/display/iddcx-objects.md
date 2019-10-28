---
title: IddCx 对象
description: IddCx 使用可扩展的 UMDF 对象模型来表示图形对象，以下各节将对这些对象进行介绍。
ms.assetid: B4D40C6B-DCEF-4661-9DF2-411326870014
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 167b521e1dbf3492b78ea771e3ef9fac274b44e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838892"
---
# <a name="iddcx-objects"></a>IddCx 对象


IddCx 使用可扩展的 UMDF 对象模型来表示图形对象，以下各节将对这些对象进行介绍。 UMDF 对象模型允许与每个 IddCx （因而是 UMDF）对象相关联的驱动程序特定的存储，有关详细信息，请参阅 UMDF 对象模型

## <a name="span-ididdcx_adapterspanspan-ididdcx_adapterspaniddcx_adapter"></a><span id="IDDCX_ADAPTER"></span><span id="iddcx_adapter"></span>IDDCX\_适配器


此对象表示由驱动程序在两阶段过程中创建的单个逻辑显示适配器。 首先，它调用[**IddCxAdapterInitAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxadapterinitasync)回调函数，并且 OS 调用驱动程序的[EvtIddCxAdapterInitFinished](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_adapter_init_finished) DDI 来完成初始化。

在最简单的情况下，附加的间接显示设备的即插即用子系统和驱动程序创建的**IDDCX\_适配器**所创建的 UMDF 设备对象之间存在一对一的映射。 在一个间接显示连接器包含多个即插即用设备（例如2个 USB 设备功能）的更复杂方案中，驱动程序只为多个 UMDF 设备创建一个**IDDCX\_适配器**对象创建的对象，每个 Pnp 设备一个。 在此方案中，驱动程序需要考虑以下事项：

1. 仅当所有组成间接显示解决方案的设备已成功启动后，才应创建**IDDCX\_适配器**
2. 在创建适配器时，驱动程序必须传递单个**WDFDEVICE** ，因此需要使用逻辑来确定它将通过哪个 UMDF 设备。
3. 如果组成间接显示适配器的任何设备都出现硬件错误，则驱动程序应报告使适配器出现错误的所有设备。
间接显示模型没有显式销毁适配器回调。 成功完成适配器初始化序列后，适配器将有效，直到在初始化时传递的 UMDF 设备停止。 创建适配器时，驱动程序提供有关间接显示适配器的静态适配器信息。

## <a name="span-ididdcx_monitorspanspan-ididdcx_monitorspaniddcx_monitor"></a><span id="IDDCX_MONITOR"></span><span id="iddcx_monitor"></span>IDDCX\_监视器


此对象表示连接到间接显示适配器上某个连接器的特定监视器。

驱动程序在两阶段过程中创建监视对象。 首先，驱动程序调用[**IddCxMonitorCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorcreate)回调来创建**IDDCX\_monitor**对象，然后调用[**IddCxMonitorArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorarrival)回调来完成监视器到达。 当拔出监视器时，驱动程序将调用[**IddCxMonitorDeparture**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitordeparture)回调以报告监视器已拔出，这将导致**IDDCX\_的监视器**对象被销毁。 即使已重新连接同一监视器，也需再次调用**IddCxMonitorDeparture**/**IddCxMonitorArrival**序列。 **IDDCX\_监视器**是**IDDCX\_适配器**对象的子对象。

## <a name="span-ididdcx_swapchainspanspan-ididdcx_swapchainspaniddcx_swapchain"></a><span id="IDDCX_SWAPCHAIN"></span><span id="iddcx_swapchain"></span>IDDCX\_存在


此对象表示一个存在，该对象将提供要在连接的监视器上显示的桌面映像。 存在有多个缓冲区，使操作系统可以在一个缓冲区中撰写下一个桌面映像，而间接显示的驱动程序则访问另一个缓冲区。 **IDDCX\_存在**是**IDDCX\_监视器**的子元素，因此，任何时候都只能有一个分配到给定监视器的存在。 OS 创建并销毁**IDDCX\_存在**对象，并将其分配/其分配到使用 EvtIddCxMonitorAssignSwapChain 和 EvtIddCxMonitorUnassignSwapChain Ddi 调用的监视器。

## <a name="span-ididdcx_opmctxspanspan-ididdcx_opmctxspaniddcx_opmctx"></a><span id="IDDCX_OPMCTX"></span><span id="iddcx_opmctx"></span>IDDCX\_OPMCTX


此对象表示来自单个应用程序 OPM 上下文的活动 OPM 上下文，应用程序可使用该上下文控制单个监视器上的输出保护。 给定监视器上的多个 OPM 上下文可以同时处于活动状态。 操作系统使用驱动程序的 EvtIddCxMonitorOPMCreateProtectedOutput 和 EvtIddCxMonitorOPMDestroyProtectedOutput DDI 调用来调用驱动程序来创建和销毁 OPM 上下文。

 

 





