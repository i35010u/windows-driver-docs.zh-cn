---
title: DirectX 图形内核子系统
description: Microsoft DirectX 图形内核子系统 (Dxgkrnl.sys) 实现微型端口驱动程序调用的函数。
ms.assetid: 7601c761-bdab-4d18-8a84-7d69a71ec41c
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: bca6196b5e14d5138e4bbb81e2a55a8756c49075
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522726"
---
# <a name="directx-graphics-kernel-subsystem-dxgkrnlsys"></a>DirectX 图形内核子系统 (Dxgkrnl.sys)

本主题概述了通过 Microsoft DirectX 图形内核子系统 (Dxgkrnl.sys) 实现的 Windows 操作系统的内核模式接口。

显示端口驱动程序是一个部分的 DirectX 图形内核子系统 (Dxgkrnl.sys)。 显示适配器供应商实现显示微型端口驱动程序。 实现 DirectX 图形内核子系统的其他功能的说明，请参阅以下主题：

[VidPN 对象和接口](vidpn-objects-and-interfaces.md)

[支持独立于路径的旋转](supporting-path-independent-rotation.md)

[获取辅助监视器目标模式](obtaining-additional-monitor-target-modes.md)

通过显示微型端口驱动程序实现的函数的说明，请参阅内核模式接口实现通过显示微型端口驱动程序。

## <a name="dxgkrnl-interface"></a>Dxgkrnl 接口

DirectX 图形内核子系统 (*Dxgkrnl.sys*) 显示微型端口驱动程序提供下表中的函数的指针通过传递[DXGKRNL_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgkrnl_interface)结构显示微型端口驱动程序[DxgkDdiStartDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)函数。 DXGKRNL_INTERFACE 结构还包含到特定的显示适配器的 （由显示器端口驱动程序生成） 的句柄。 显示微型端口驱动程序作为参数调用任何函数中 DXGKRNL_INTERFACE 每次将传递该句柄。



|Dxgkrnl.sys||
|:---|:---|
|DxgkInitialize|（仅由内核模式仅显示驱动程序调用） 的 DxgkInitializeDisplayOnlyDriver (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbAcquirePostDisplayOwnership (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbCompleteFStateTransition (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbCreateContextAllocation (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbDestroyContextAllocation (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbEnumHandleChildren|DxgkCbEvalAcpiMethod|
|DxgkCbExcludeAdapterAccess|DxgkCbGetCaptureAddress|
|DxgkCbGetDeviceInformation|DxgkCbGetHandleData|
|DxgkCbGetHandleParent|DxgkCbIndicateChildStatus|
|DxgkCbIsDevicePresent|DxgkCbLogEtwEvent|
|DxgkCbMapMemory|DxgkCbNotifyDpc|
|DxgkCbNotifyInterrupt|DxgkCbPowerRuntimeControlRequest (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|
|（仅由内核模式仅显示驱动程序调用） 的 DxgkCbPresentDisplayOnlyProgress (DXGKDDI_INTERFACE_VERSION > = DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbQueryMonitorInterface|
|DxgkCbQueryServices|DxgkCbQueryVidPnInterface|
|DxgkCbQueueDpc|DxgkCbReadDeviceSpace|
|DxgkCbSetPowerComponentActive (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbSetPowerComponentIdle (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|
|DxgkCbSetPowerComponentLatency (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|DxgkCbSetPowerComponentResidency (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8)|
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

以下函数由操作系统实现，由显示微型端口驱动程序以支持 AGP （加速的图形端口） 调用。 显示微型端口驱动程序通过将 DxgkServicesAgp 值传递到 DXGK_SERVICES 枚举类型来获取这些函数的指针*ServicesType*参数的[DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_query_services)函数。

|AGP 函数|
|:---|
|[AgpAllocatePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_agp_allocate_pool)|
|[AgpFreePool](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_agp_free_pool)|
|[AgpSetCommand](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_agp_set_command)|


## <a name="debug-report-interface"></a>调试报表接口


显示微型端口驱动程序获取指向以下函数通过传递*DxgkServicesDebugReport* DXGK_SERVICES 枚举类型设置为值*ServicesType*参数[DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_query_services)函数。 这些函数通过访问[_DXGK_DEBUG_REPORT_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_debug_report_interface)结构。

|调试报告函数|
|:---|
|DbgReportComplete|
|DbgReportCreate|
|DbgReportSecondaryData|

## <a name="timed-operation-interface"></a>定时的操作接口

显示微型端口驱动程序获取指向以下函数通过传递*DxgkServicesTimedOperation* DXGK_SERVICES 枚举类型设置为值*ServicesType*参数[DxgkCbQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_query_services)函数。 DxgkCbQueryServices 中前面的列表中的成员函数返回指向[DXGK_TIMED_OPERATION_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_timed_operation_interface)结构; 显示微型端口驱动程序提供一个指向到 DXGK_TIMED_OPERATION_INTERFACE*接口*DxgkCbQueryServices 参数。

|定时的操作函数|
|:---|
|TimedOperationStart|
|TimedOperationDelay|
|TimedOperationWaitForSingleObject|

## <a name="see-also"></a>另请参阅

[Windows 显示驱动程序模型 (WDDM) 体系结构](windows-vista-and-later-display-driver-model-architecture.md)

[初始化显示微型端口驱动程序](initializing-the-display-miniport-driver.md)

