---
title: DirectX 图形内核子系统
description: 'Microsoft DirectX 图形内核子系统 ( # A0) 实现了显示微型端口驱动程序调用的函数。'
ms.assetid: 7601c761-bdab-4d18-8a84-7d69a71ec41c
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: cc2c5af36e3b8e7bfb5db11f99c66d35f98809ed
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063122"
---
# <a name="directx-graphics-kernel-subsystem-dxgkrnlsys"></a>DirectX 图形内核子系统 ( # A0) 

本主题列出了 Windows 操作系统通过 Microsoft DirectX 图形内核子系统实现 ( # A0) 的内核模式接口。

显示端口驱动程序是 ( # A0) 的 DirectX 图形内核子系统的一个部分。 显示微型端口驱动程序由显示适配器供应商实现。 有关 DirectX 图形内核子系统实现的其他功能的说明，请参阅以下主题：

[VidPN 对象和接口](vidpn-objects-and-interfaces.md)

[支持独立于路径的旋转](supporting-path-independent-rotation.md)

[获取其他监视目标模式](obtaining-additional-monitor-target-modes.md)

有关显示微型端口驱动程序实现的函数的说明，请参阅显示微型端口驱动程序实现的内核模式接口。

## <a name="dxgkrnl-interface"></a>Dxgkrnl 接口

DirectX 图形内核子系统 (*Dxgkrnl.sys*) 通过将 [DXGKRNL_INTERFACE](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgkrnl_interface) 结构传递到显示微型端口驱动程序的 [DxgkDdiStartDevice](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device) 函数，向显示微型端口驱动程序提供指向下表中的函数的指针。 DXGKRNL_INTERFACE 结构还包含显示端口驱动程序 (生成的句柄，) 到特定显示适配器。 每次调用 DXGKRNL_INTERFACE 中的任何函数时，显示微型端口驱动程序都将该句柄作为参数传递。

* DxgkInitialize
* DxgkInitializeDisplayOnlyDriver (仅由内核模式仅显示驱动程序)  (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8 调用) 
* DxgkCbAcquirePostDisplayOwnership (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbCompleteFStateTransition (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbCreateContextAllocation (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbDestroyContextAllocation (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbEnumHandleChildren
* DxgkCbEvalAcpiMethod
* DxgkCbExcludeAdapterAccess
* DxgkCbGetCaptureAddress
* DxgkCbGetDeviceInformation
* DxgkCbGetHandleData
* DxgkCbGetHandleParent
* DxgkCbIndicateChildStatus
* DxgkCbIsDevicePresent
* DxgkCbLogEtwEvent
* DxgkCbMapMemory
* DxgkCbNotifyDpc
* DxgkCbNotifyInterrupt
* DxgkCbPowerRuntimeControlRequest (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbPresentDisplayOnlyProgress (仅由内核模式仅显示驱动程序)  (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8 调用) 
* DxgkCbQueryMonitorInterface
* DxgkCbQueryServices
* DxgkCbQueryVidPnInterface
* DxgkCbQueueDpc
* DxgkCbReadDeviceSpace
* DxgkCbSetPowerComponentActive (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbSetPowerComponentIdle (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbSetPowerComponentLatency (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbSetPowerComponentResidency (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WIN8) 
* DxgkCbSynchronizeExecution
* DxgkCbUnmapMemory
* DxgkCbWriteDeviceSpace
* DxgkCbIsDevicePresent
* DxgkCbGetHandleData
* DxgkCbGetHandleParent
* DxgkCbEnumHandleChildren
* DxgkCbNotifyInterrupt
* DxgkCbNotifyDpc
* DxgkCbQueryVidPnInterface
* DxgkCbQueryMonitorInterface
* DxgkCbGetCaptureAddress
* DxgkCbLogEtwEvent
* DxgkCbExcludeAdapterAccess
* DxgkCbCreateContextAllocation
* DxgkCbDestroyContextAllocation
* DxgkCbSetPowerComponentActive
* DxgkCbSetPowerComponentIdle
* DxgkCbPowerRuntimeControlRequest

## <a name="agp-interface"></a>AGP 接口

以下函数由操作系统实现并由显示微型端口驱动程序调用以支持 AGP (加速图形端口) 。 显示微型端口驱动程序通过将 DxgkServicesAgp 值从 DXGK_SERVICES 枚举类型传递到[DxgkCbQueryServices](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)函数的*ServicesType*参数，获取指向这些函数的指针。

* [AgpAllocatePool](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_allocate_pool)
* [AgpFreePool](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_free_pool)
* [AgpSetCommand](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_agp_set_command)


## <a name="debug-report-interface"></a>调试报表接口


显示微型端口驱动程序通过将*DxgkServicesDebugReport*值从 DXGK_SERVICES 枚举类型传递到[DxgkCbQueryServices](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)函数的*ServicesType*参数，获取指向以下函数的指针。 这些函数通过 [_DXGK_DEBUG_REPORT_INTERFACE](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_debug_report_interface) 结构进行访问。

* DbgReportComplete
* DbgReportCreate
* DbgReportSecondaryData

## <a name="timed-operation-interface"></a>计时操作接口

显示微型端口驱动程序通过将*DxgkServicesTimedOperation*值从 DXGK_SERVICES 枚举类型传递到[DxgkCbQueryServices](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_query_services)函数的*ServicesType*参数，获取指向以下函数的指针。 DxgkCbQueryServices 返回指向 [DXGK_TIMED_OPERATION_INTERFACE](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_timed_operation_interface) 结构成员的前一列表中的函数的指针;显示微型端口驱动程序提供了一个指向 DxgkCbQueryServices 的 *INTERFACE* 参数 DXGK_TIMED_OPERATION_INTERFACE 的指针。

* TimedOperationStart
* TimedOperationDelay
* TimedOperationWaitForSingleObject

## <a name="see-also"></a>另请参阅

[Windows 显示驱动程序模型 (WDDM) 体系结构](windows-vista-and-later-display-driver-model-architecture.md)

[初始化显示微型端口驱动程序](initializing-the-display-miniport-driver.md)