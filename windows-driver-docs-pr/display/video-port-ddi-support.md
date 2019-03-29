---
title: 视频端口 DDI 支持
description: 从 Windows 8 开始，基于在 Windows 2000 显示驱动程序模型 (XDDM) 一起显示驱动程序不会安装或运行，但 GDI 辅助功能驱动程序和远程显示器驱动程序将安装并运行。
ms.assetid: 87A98A49-B01B-419D-B570-6ECA60E2C7AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3e12ad56ee5992084db2ba72dfc4ddbb797689a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566913"
---
# <a name="video-port-ddi-support"></a>视频端口 DDI 支持


从 Windows 8 开始显示驱动程序基于[Windows 2000 显示驱动程序模型 (XDDM)](windows-2000-display-driver-model-design-guide.md)不会安装或运行，但[GDI 辅助功能驱动程序](mirror-drivers.md)和[远程显示器驱动程序](remote-display-drivers.md)将安装并运行。 对于这种情况都支持仅某些由视频端口驱动程序导出的函数。

## <a name="span-idsupportedvideoportddisspanspan-idsupportedvideoportddisspanspan-idsupportedvideoportddisspansupported-video-port-ddis"></a><span id="Supported_Video_Port_DDIs"></span><span id="supported_video_port_ddis"></span><span id="SUPPORTED_VIDEO_PORT_DDIS"></span>受支持的视频端口 DDIs


GDI 辅助功能驱动程序和远程显示驱动程序的情况下，从 Windows 8 仍支持以下系统实现视频端口驱动程序设备驱动程序接口 (DDIs) 开始。

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

## <a name="span-idunsupportedvideoportddisspanspan-idunsupportedvideoportddisspanspan-idunsupportedvideoportddisspanunsupported-video-port-ddis"></a><span id="Unsupported_Video_Port_DDIs"></span><span id="unsupported_video_port_ddis"></span><span id="UNSUPPORTED_VIDEO_PORT_DDIS"></span>不支持的视频端口 DDIs


有关 GDI 辅助功能驱动程序和远程显示驱动程序方案，不支持以下系统实现视频端口驱动程序 DDIs 开始 Windows 8。

项标有星号 (\*) 适用于从 Windows 8 开始不再支持的硬件方案。

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

 

 





