---
title: DirectX 图形内核子系统
description: Microsoft DirectX graphics 内核子系统（Dxgkrnl）实现了显示微型端口驱动程序调用的函数。
ms.assetid: 7601c761-bdab-4d18-8a84-7d69a71ec41c
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: d051988e63a6528322358d4616f46b8ab91d1654
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838996"
---
# <a name="directx-graphics-kernel-subsystem-dxgkrnlsys"></a>DirectX 图形内核子系统（Dxgkrnl）

本主题概述 Windows 操作系统通过 Microsoft DirectX 图形内核子系统（Dxgkrnl）实现的内核模式接口。

显示端口驱动程序是 DirectX 图形内核子系统（Dxgkrnl）的一部分。 显示微型端口驱动程序由显示适配器供应商实现。 有关 DirectX 图形内核子系统实现的其他功能的说明，请参阅以下主题：

[VidPN 对象和接口](vidpn-objects-and-interfaces.md)

[支持独立于路径的旋转](supporting-path-independent-rotation.md)

[获取更多监视目标模式](obtaining-additional-monitor-target-modes.md)

有关显示微型端口驱动程序实现的函数的说明，请参阅显示微型端口驱动程序实现的内核模式接口。

## <a name="dxgkrnl-interface"></a>Dxgkrnl 接口

DirectX 图形内核子系统（*Dxgkrnl*）通过将[DXGKRNL_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgkrnl_interface)结构传递到显示微型端口驱动程序的[，提供显示微型端口驱动程序，其中包含指向下表中函数的指针DxgkDdiStartDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)函数。 DXGKRNL_INTERFACE 结构还包含指向特定显示适配器的句柄（由显示端口驱动程序生成）。 每次调用 DXGKRNL_INTERFACE 中的任何函数时，显示微型端口驱动程序会将该句柄作为参数传递。



|Dxgkrnl||
|:---|:---|
|DxgkInitialize|DxgkInitializeDisplayOnlyDriver （仅由内核模式仅显示驱动程序调用）（DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|
|DxgkCbAcquirePostDisplayOwnership （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|DxgkCbCompleteFStateTransition （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|
|DxgkCbCreateContextAllocation （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|DxgkCbDestroyContextAllocation （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|
|DxgkCbEnumHandleChildren|DxgkCbEvalAcpiMethod|
|DxgkCbExcludeAdapterAccess|DxgkCbGetCaptureAddress|
|DxgkCbGetDeviceInformation|DxgkCbGetHandleData|
|DxgkCbGetHandleParent|DxgkCbIndicateChildStatus|
|DxgkCbIsDevicePresent|DxgkCbLogEtwEvent|
|DxgkCbMapMemory|DxgkCbNotifyDpc|
|DxgkCbNotifyInterrupt|DxgkCbPowerRuntimeControlRequest （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|
|DxgkCbPresentDisplayOnlyProgress （仅由内核模式仅显示驱动程序调用）（DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|DxgkCbQueryMonitorInterface|
|DxgkCbQueryServices|DxgkCbQueryVidPnInterface|
|DxgkCbQueueDpc|DxgkCbReadDeviceSpace|
|DxgkCbSetPowerComponentActive （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|DxgkCbSetPowerComponentIdle （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|
|DxgkCbSetPowerComponentLatency （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|DxgkCbSetPowerComponentResidency （DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8）|
|DxgkCbSynchronizeExecution|DxgkCbUnmapMemory|
|DxgkCbWriteDeviceSpace|DxgkCbIsDevicePresent|
|DxgkCbGetHandleData|DxgkCbGetHandleParent|
|DxgkCbEnumHandleChildren|DxgkCbNotifyInterrupt|
|DxgkCbNotifyDpc|DxgkCbQueryVidPnInterface|
|DxgkCbQueryMonitorInterface|DxgkCbGetCaptureAddress|
|DxgkCbLogEtwEvent|DxgkCbExcludeAdapterAccess|
|DxgkCbCreateContextAllocation|DxgkCbDestroyContextAllocation|
|DxgkCbSetPowerComponentActive|DxgkCbSetPowerComponentIdle|
|DxgkCbPowerRuntimeControlRequest||

## <a name="agp-interface"></a>AGP 接口

以下函数由操作系统实现并由显示微型端口驱动程序调用以支持 AGP （加速图形端口）。 显示微型端口驱动程序通过将 DxgkServicesAgp 值从 DXGK_SERVICES 枚举类型传递到[DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)函数的*ServicesType*参数，获取指向这些函数的指针。

|AGP 函数|
|:---|
|[AgpAllocatePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_allocate_pool)|
|[AgpFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_free_pool)|
|[AgpSetCommand](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_set_command)|


## <a name="debug-report-interface"></a>调试报表接口


显示微型端口驱动程序通过将*DxgkServicesDebugReport*值从 DXGK_SERVICES 枚举类型传递到[DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)函数的*ServicesType*参数，获取指向以下函数的指针。 这些函数通过[_DXGK_DEBUG_REPORT_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_debug_report_interface)结构访问。

|调试报表功能|
|:---|
|DbgReportComplete|
|DbgReportCreate|
|DbgReportSecondaryData|

## <a name="timed-operation-interface"></a>计时操作接口

显示微型端口驱动程序通过将*DxgkServicesTimedOperation*值从 DXGK_SERVICES 枚举类型传递到[DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)函数的*ServicesType*参数，获取指向以下函数的指针. DxgkCbQueryServices 返回指向[DXGK_TIMED_OPERATION_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_timed_operation_interface)结构的成员中前面列表中函数的指针;显示微型端口驱动程序提供指向 DxgkCbQueryServices 的*INTERFACE*参数的 DXGK_TIMED_OPERATION_INTERFACE 的指针。

|计时运算函数|
|:---|
|TimedOperationStart|
|TimedOperationDelay|
|TimedOperationWaitForSingleObject|

## <a name="see-also"></a>另请参阅

[Windows 显示驱动程序模型（WDDM）体系结构](windows-vista-and-later-display-driver-model-architecture.md)

[正在初始化显示微型端口驱动程序](initializing-the-display-miniport-driver.md)

