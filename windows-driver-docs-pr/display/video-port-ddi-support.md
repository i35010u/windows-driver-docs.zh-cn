---
title: 视频端口 DDI 支持
description: 从 Windows 8 开始，基于 Windows 2000 显示器驱动程序模型显示驱动程序 (XDDM) 将不会安装或运行，但 GDI 辅助功能驱动程序和远程显示驱动程序将安装并运行。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39e94bab5c95df81c0f4116feefa44c3dbc14aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824161"
---
# <a name="video-port-ddi-support"></a>视频端口 DDI 支持


从 Windows 8 开始，基于 [windows 2000 显示器驱动程序模型显示驱动程序 (XDDM) ](windows-2000-display-driver-model-design-guide.md) 将不会安装或运行，但 [GDI 辅助功能驱动程序](mirror-drivers.md) 和 [远程显示驱动](remote-display-drivers.md) 程序将安装并运行。 对于这些方案，只支持视频端口驱动程序导出的某些函数。

## <a name="span-idsupported_video_port_ddisspanspan-idsupported_video_port_ddisspanspan-idsupported_video_port_ddisspansupported-video-port-ddis"></a><span id="Supported_Video_Port_DDIs"></span><span id="supported_video_port_ddis"></span><span id="SUPPORTED_VIDEO_PORT_DDIS"></span>支持的视频端口 DDIs


对于 GDI 辅助功能驱动程序和远程显示驱动程序方案，从 Windows 8 开始，仍支持以下系统实现的视频端口驱动程序设备驱动程序接口 (DDIs) 。

-   VideoDebugPrint
-   VideoPortAcquireDeviceLock
-   VideoPortAcquireSpinLock
-   VideoPortAcquireSpinLockAtDpcLevel
-   VideoPortAllocatePool
-   VideoPortClearEvent
-   VideoPortCompareMemory
-   VideoPortCreateEvent
-   VideoPortCreateSpinLock
-   VideoPortDeleteEvent
-   VideoPortDeleteSpinLock
-   VideoPortFlushRegistry
-   VideoPortFreePool
-   VideoPortGetAssociatedDeviceExtension
-   VideoPortGetCurrentIrql
-   VideoPortGetProcAddress
-   VideoPortGetRegistryParameters
-   VideoPortGetVersion
-   VideoPortInterlockedDecrement
-   VideoPortInterlockedExchange
-   VideoPortInterlockedIncrement
-   VideoPortInitialize
-   VideoPortLockBuffer
-   VideoPortLogError
-   VideoPortMoveMemory
-   VideoPortQueryPerformanceCounter
-   VideoPortQueryServices
-   VideoPortQuerySystemTime
-   VideoPortQueueDpc
-   VideoPortReadStateEvent
-   VideoPortReleaseDeviceLock
-   VideoPortReleaseSpinLock
-   VideoPortReleaseSpinLockFromDpcLevel
-   VideoPortSetEvent
-   VideoPortSetRegistryParameters
-   VideoPortSynchronizeExecution
-   VideoPortUnlockBuffer
-   VideoPortWaitForSingleObject
-   VideoPortZeroMemory

## <a name="span-idunsupported_video_port_ddisspanspan-idunsupported_video_port_ddisspanspan-idunsupported_video_port_ddisspanunsupported-video-port-ddis"></a><span id="Unsupported_Video_Port_DDIs"></span><span id="unsupported_video_port_ddis"></span><span id="UNSUPPORTED_VIDEO_PORT_DDIS"></span>不支持的视频端口 DDIs


对于 GDI 辅助功能驱动程序和远程显示驱动程序方案，从 Windows 8 开始，不支持以下系统实现的视频端口驱动程序 DDIs。

用星号 () 标记的项 \* 适用于从 Windows 8 开始不再支持的硬件方案。

-   VideoPortAllocateBuffer
-   VideoPortAllocateCommonBuffer
-   VideoPortAllocateContiguousMemory
-   VideoPortAssociateEventsWithDmaHandle
-   VideoPortCheckForDeviceExistence\*
-   VideoPortCompleteDma\*
-   VideoPortCreateSecondaryDisplay\*
-   VideoPortDDCMonitorHelper\*
-   VideoPortDebugPrint
-   VideoPortDisableInterrupt
-   VideoPortDoDma
-   VideoPortEnableInterrupt
-   VideoPortEnumerateChildren\*
-   VideoPortFreeCommonBuffer
-   VideoPortFreeDeviceBase\*
-   VideoPortGetAccessRanges\*
-   VideoPortGetAgpServices
-   VideoPortGetAssociatedDeviceID\*
-   VideoPortGetBusData\*
-   VideoPortGetBytesUsed
-   VideoPortGetCommonBuffer
-   VideoPortGetDeviceBase\*
-   VideoPortGetDeviceData\*
-   VideoPortGetDmaAdapter\*
-   VideoPortGetDmaContext
-   VideoPortGetMdl
-   VideoPortGetRomImage\*
-   VideoPortGetVgaStatus\*
-   VideoPortInt10\*
-   VideoPortIsNoVesa\*
-   VideoPortLockPages
-   VideoPortMapBankedMemory
-   VideoPortMapDmaMemory
-   VideoPortMapMemory\*
-   VideoPortProtectWCMemory\*
-   VideoPortPutDmaAdapter\*
-   VideoPortReadPortBufferUchar\*
-   VideoPortReadPortBufferUlong\*
-   VideoPortReadPortBufferUshort\*
-   VideoPortReadPortUchar\*
-   VideoPortReadPortUlong\*
-   VideoPortReadPortUshort\*
-   VideoPortReadRegisterBufferUchar
-   VideoPortReadRegisterBufferUlong
-   VideoPortReadRegisterBufferUshort
-   VideoPortReadRegisterUchar
-   VideoPortReadRegisterUlong
-   VideoPortReadRegisterUshort
-   VideoPortRegisterBugcheckCallback
-   VideoPortReleaseBuffer
-   VideoPortReleaseCommonBuffer\*
-   VideoPortRestoreWCMemory\*
-   VideoPortScanRom\*
-   VideoPortSetBusData\*
-   VideoPortSetBytesUsed
-   VideoPortSetDmaContext
-   VideoPortSetTrappedEmulatorPorts\*
-   VideoPortSignalDmaComplete
-   VideoPortStallExecution
-   VideoPortStartDma\*
-   VideoPortStartTimer
-   VideoPortStopTimer
-   VideoPortUnlockPages
-   VideoPortUnmapDmaMemory
-   VideoPortUnmapMemory\*
-   VideoPortVerifyAccessRanges\*
-   VideoPortWritePortBufferUchar\*
-   VideoPortWritePortBufferUlong\*
-   VideoPortWritePortBufferUshort\*
-   VideoPortWritePortUchar\*
-   VideoPortWritePortUlong\*
-   VideoPortWritePortUshort\*
-   VideoPortWriteRegisterBufferUchar
-   VideoPortWriteRegisterBufferUlong
-   VideoPortWriteRegisterBufferUshort
-   VideoPortWriteRegisterUchar
-   VideoPortWriteRegisterUlong
-   VideoPortWriteRegisterUshort
-   VideoPortZeroDeviceMemory\*

 

 





