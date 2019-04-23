---
title: KMDF 版本历史记录
description: 本主题列出了版本的内核模式驱动程序框架 (KMDF) 的相应版本的 Windows 操作系统，并在每个版本中所做的更改。
ms.assetid: b920937c-2e5d-48cc-81b5-1462f5d03d75
keywords:
- 内核模式驱动程序 WDK KMDF，修订版本历史记录
- KMDF WDK，修订版本历史记录
- 内核模式驱动程序框架 WDK，修订版本历史记录
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 358d5eb53fc4005f17577f79c2644b2074423ae4
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903067"
---
# <a name="kmdf-version-history"></a>KMDF 版本历史记录


本主题列出了版本的内核模式驱动程序框架 (KMDF) 的相应版本的 Windows 操作系统，并在每个版本中所做的更改。

下表显示了 KMDF 库的版本历史记录：

|KMDF 版本|Release 方法|包含在此版本的 Windows|使用它的驱动程序上运行|
|--- |--- |--- |--- |
|1.29|不在 WDK 中发布|Windows 10，版本 1903年 （2019 更新，19 H 1 年 3 月）|Windows 10，版本 1903 及更高版本|
|1.27|Windows 10，版本 1809 WDK|Windows 10，版本 1809年 (2018 年 10 月更新 Redstone 5)|Windows 10，版本 1809 及更高版本|
|1.25|Windows 10，版本 1803 WDK|Windows 10，版本 1803年 (2018 年 4 月更新 Redstone 4)|Windows 10，版本 1803 和更高版本|
|1.23|Windows 10 版本 1709 WDK|Windows 10 版本 1709 （Fall Creators Update，Redstone 3）|Windows 10 版本 1709 及更高版本|
|1.21|Windows 10，版本 1703 WDK|Windows 10，版本 1703 （创意者更新，Redstone 2）|Windows 10 版本 1703 及更高版本|
|1.19|Windows 10，版本 1607 WDK|Windows 10，版本 1607 （周年更新，Redstone 1）|Windows 10 版本 1607，Windows Server 2016 及更高版本|
|1.17|Windows 10 版本 1511 WDK|Windows 10 版本 1511 （11 月更新，阈值 2）|Windows 10 版本 1511，Windows Server 2016 及更高版本|
|1.15|Windows 10 WDK|Windows 10 版本 1507 (阈值 1)|Windows 10，版本 1507，Windows Server 2016 及更高版本|
|1.13|Windows 8.1 WDK|Windows 8.1|Windows 8.1 及更高版本|
|1.11|Windows 8 WDK|Windows 8|Windows Vista 及更高版本|
|1.9|Windows 7 WDK|Windows 7|Windows XP 及更高版本|
|1.7|Windows Server 2008 WDK|Windows Vista Service Pack 1 (SP1)，Windows Server 2008|Windows 2000 及更高版本|
|1.5|Windows Vista WDK|Windows Vista|Windows 2000 及更高版本|
|1.1|仅下载|无|Windows 2000 及更高版本|
|1.0|仅下载|无|Windows XP 及更高版本|

可以使用 Microsoft Visual Studio 2017 中使用 Windows Driver Kit (WDK) 来构建运行 Windows 7 及更高版本的驱动程序。

回调的完整列表和方法，以及哪个框架和它们适用于版本，请参阅[WDF 回调摘要和方法](https://msdn.microsoft.com/library/windows/hardware/dn265591)。

用于 KMDF 驱动程序在 Windows 10 中的新功能的信息，请参阅[What's New for WDF 驱动程序](index.md)。

## <a name="kmdf-version-129"></a>KMDF 1.29 版

从版本 1.25 不变。

## <a name="kmdf-version-127"></a>KMDF 版本 1.27 版

从版本 1.25 不变。

## <a name="kmdf-version-125"></a>KMDF 版本 1.25

* [针对多个 Windows 版本生成 WDF 驱动程序](building-a-wdf-driver-for-multiple-versions-of-windows.md)

## <a name="kmdf-version-123"></a>KMDF 版本 1.23

* 仅供内部使用已添加的配套功能。  有关新 DDIs，请参阅[WDF 回调摘要和方法](https://msdn.microsoft.com/library/windows/hardware/dn265591)。

## <a name="kmdf-version-121"></a>KMDF 版本 1.21

* [**WdfFileObjectGetInitiatorProcessId** ](https://msdn.microsoft.com/library/windows/hardware/dn265614)以前仅 UMDF，现已在 KMDF。
* [**WdfRequestGetRequestorProcessId** ](https://msdn.microsoft.com/library/windows/hardware/dn265617)以前仅 UMDF，现已在 KMDF。
* [**WdfObjectDereferenceActual**](https://msdn.microsoft.com/library/windows/hardware/ff548743):类型*文件*参数从 PCHAR 更改为 PCCH。
* [**WdfObjectReferenceActual**](https://msdn.microsoft.com/library/windows/hardware/ff548760):类型*文件*参数从 PCHAR 更改为 PCCH。

## <a name="kmdf-version-119"></a>KMDF 版本 1.19

* Added [**WdfDmaTransactionSetSingleTransferRequirement**](https://msdn.microsoft.com/library/windows/hardware/988c7e70-3b2a-4a0f-91cf-dfab3ea07f05)
* 添加**WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**中的标志[ **WDF_DMA_ENABLER_CONFIG_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/hh439491)
* 添加**STATUS_WDF_TOO_MANY_TRANSFERS**返回的值[ **WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)并[ **WdfDmaTransactionDmaCompleted**](https://msdn.microsoft.com/library/windows/hardware/ff547039)
* 添加到单个传输输出的输出消息[ **！ wdfkd.wdfdmatransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff565721)并[ **！ wdfkd.wdfdmaenabler**](https://msdn.microsoft.com/library/windows/hardware/ff565717)
* 有关单个传输 DMA 的详细信息，请参阅[使用单个传输 DMA](using-single-transfer-dma.md)。

## <a name="kmdf-version-115"></a>KMDF 版本 1.15

-   新[ **WdfDeviceOpenDevicemapKey** ](https://msdn.microsoft.com/library/windows/hardware/dn932458)方法允许驱动程序添加到访问子项和值下**HKEY\_本地\_机\\硬件\\DEVICEMAP**。

## <a name="kmdf-version-113"></a>KMDF 版本 1.13


版本 1.13 KMDF 新增了以下功能：

-   添加**CanWakeDevice**成员添加到[ **WDF\_中断\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552347)结构，以支持可用于将从设备的中断恢复到其完全处于 D0 状态低功耗 Dx 状态。 有关详细信息，请参阅[中断用于唤醒设备](using-an-interrupt-to-wake-a-device.md)。
-   对高分辨率计时器的支持。 有关详细信息，请参阅[使用计时器](using-timers.md)。
-   如果在过期时系统处于低功耗状态无法唤醒系统计时器的支持。 有关详细信息，请参阅[使用计时器](using-timers.md)。
-   以下 KMDF/UMDF 方法中所述[访问统一的设备属性模型](accessing-the-unified-device-property-model.md):
    -   [**WdfDeviceAllocAndQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265599)
    -   [**WdfDeviceAssignProperty**](https://msdn.microsoft.com/library/windows/hardware/dn265601)
    -   [**WdfDeviceInitSetIoTypeEx**](https://msdn.microsoft.com/library/windows/hardware/dn265604)
    -   [**WdfDeviceQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265608)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265612)
    -   [**WdfFdoInitQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265613)

UMDF 版本有关的信息，请参阅[UMDF 版本历史记录](umdf-version-history.md)。

## <a name="kmdf-version-111"></a>KMDF 版本 1.11


1.11 版新增了以下功能：

-   [System-mode DMA](supporting-system-mode-dma.md)

-   支持[被动等级中断](supporting-passive-level-interrupts.md)

-   [功能的电源状态](supporting-functional-power-states.md)内单个设备的多个组件

-   [调度到的 I/O 队列的 Irp](dispatching-irps-to-i-o-queues.md)
-   以下方法：
    -   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://msdn.microsoft.com/library/windows/hardware/hh451093)
    -   [**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://msdn.microsoft.com/library/windows/hardware/hh706196)
    -   [**WdfDeviceInitSetRemoveLockOptions**](https://msdn.microsoft.com/library/windows/hardware/hh451095)
    -   [**WdfDeviceWdmDispatchIrp**](https://msdn.microsoft.com/library/windows/hardware/hh451100)
    -   [**WdfDmaEnablerConfigureSystemProfile**](https://msdn.microsoft.com/library/windows/hardware/hh451108)
    -   [**WdfDmaTransactionAllocateResources**](https://msdn.microsoft.com/library/windows/hardware/hh451123)
    -   [**WdfDmaTransactionCancel**](https://msdn.microsoft.com/library/windows/hardware/hh451127)
    -   [**WdfDmaTransactionFreeResources**](https://msdn.microsoft.com/library/windows/hardware/hh451177)
    -   [**WdfDmaTransactionGetTransferInfo**](https://msdn.microsoft.com/library/windows/hardware/hh451179)
    -   [**WdfDmaTransactionInitializeUsingOffset**](https://msdn.microsoft.com/library/windows/hardware/hh451182)
    -   [**WdfDmaTransactionSetChannelConfigurationCallback**](https://msdn.microsoft.com/library/windows/hardware/hh451184)
    -   [**WdfDmaTransactionSetDeviceAddressOffset**](https://msdn.microsoft.com/library/windows/hardware/hh451188)
    -   [**WdfDmaTransactionSetImmediateExecution**](https://msdn.microsoft.com/library/windows/hardware/hh451190)
    -   [**WdfDmaTransactionSetTransferCompleteCallback**](https://msdn.microsoft.com/library/windows/hardware/hh439261)
    -   [**WdfDmaTransactionWdmGetTransferContext**](https://msdn.microsoft.com/library/windows/hardware/hh439267)
    -   [**WdfInterruptQueueWorkItemForIsr**](https://msdn.microsoft.com/library/windows/hardware/hh439270)
    -   [**WdfInterruptReportActive**](https://msdn.microsoft.com/library/windows/hardware/hh439273)
    -   [**WdfInterruptReportInactive**](https://msdn.microsoft.com/library/windows/hardware/hh439277)
    -   [**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)
    -   [**WdfIoQueueStopAndPurge**](https://msdn.microsoft.com/library/windows/hardware/hh439289)
    -   [**WdfIoQueueStopAndPurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/hh439293)
    -   [**WdfIoTargetPurge**](https://msdn.microsoft.com/library/windows/hardware/hh439338)
    -   [**WdfUsbTargetDeviceCreateIsochUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439420)
    -   [**WdfUsbTargetDeviceCreateUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439423)
    -   [**WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)
    -   [**WdfUsbTargetDeviceQueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh439434)
-   添加[ *EvtDeviceUsageNotificationEx*](https://msdn.microsoft.com/library/windows/hardware/hh406365)。

-   添加**IdleTimeoutType**并**ExcludeD3Cold**成员[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff551270)。

-   添加**ReportInactiveOnPowerDown**成员添加到[ **WDF\_中断\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552347)。

-   添加**WdfIoTargetPurged**值设置为[ **WDF\_IO\_目标\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff552390)。

-   添加**WdfSpecialFileBoot**值设置为[ **WDF\_特殊\_文件\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff552509)。

-   添加**DbgWaitForSignalTimeoutInSec**到[调试基于 Framework 的驱动程序的注册表值](registry-values-for-debugging-kmdf-drivers.md)。

-   添加[InstallWdf](https://go.microsoft.com/fwlink/p/?linkid=256122)， [MultiComp](https://go.microsoft.com/fwlink/p/?linkid=256158)，并[SingleComp](https://go.microsoft.com/fwlink/p/?linkid=256158)示例。

## <a name="kmdf-version-19"></a>KMDF 1.9 版


1.9 版中新增了以下功能：

-   [保证向前推进](guaranteeing-forward-progress-of-i-o-operations.md)I/O 队列

-   为支持[排队 I/O 请求](requeuing-i-o-requests.md)从子设备的 I/O 队列向父设备的 I/O 队列

-   指定功能[队列级别同步](https://msdn.microsoft.com/library/windows/hardware/ff552518)为单独的队列对象。

-   以下方法：
    -   [**WdfDeviceGetSystemPowerAction**](https://msdn.microsoft.com/library/windows/hardware/ff546022)
    -   [**WdfDeviceRemoveDependentUsageDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff546829)
    -   [**WdfInterruptSetExtendedPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff547381)
    -   [**WdfPdoInitAllowForwardingRequestToParent**](https://msdn.microsoft.com/library/windows/hardware/ff548789)
    -   [**WdfPdoInitAssignContainerID**](https://msdn.microsoft.com/library/windows/hardware/ff548792)
    -   [**WdfPreDeviceInstallEx**](https://msdn.microsoft.com/library/windows/hardware/ff548839)
    -   [**WdfRequestForwardToParentDeviceIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549959)
    -   [**WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)
-   添加**NumberOfPresentedRequests**成员添加到[ **WDF\_IO\_队列\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构，因此驱动程序可以限制该框架提供并行的 I/O 队列从驱动程序请求的 I/O 数。

-   添加**WdfFileObjectCanBeOptional**标记，用于[ **WDF\_的文件对象\_类**](https://msdn.microsoft.com/library/windows/hardware/ff551315)结构。

-   添加**TolerableDelay**成员添加到[ **WDF\_计时器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552519)结构。

-   添加[WdfDefaultIdleInWorkingState 和 WdfDefaultWakeFromSleepState](user-control-of-device-idle-and-wake-behavior.md)注册表值。

## <a name="kmdf-version-17"></a>KMDF 1.7 版


-   [ **WdfDeviceEnqueueRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff545945)方法可以调用在 IRQL&lt;= 调度\_级别。

-   [ **WdfWorkItemEnqueue** ](https://msdn.microsoft.com/library/windows/hardware/ff551203)可以调用方法，如果指定的工作项已在工作项队列上。

-   添加[ *EvtDeviceArmWakeFromSxWithReason* ](https://msdn.microsoft.com/library/windows/hardware/ff540846)事件回调函数。

-   添加**ArmForWakeIfChildrenAreArmedForWake**并**IndicateChildWakeOnParentWake**成员[ **WDF\_设备\_POWER\_策略\_唤醒\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff551277)结构。

## <a name="kmdf-version-15"></a>KMDF 版本 1.5


-   [**WdfUsbInterfaceGetNumSettings**](https://msdn.microsoft.com/library/windows/hardware/ff550070)

-   添加**DriverPoolTag**成员添加到[ **WDF\_驱动程序\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551300)。

## <a name="kmdf-version-11"></a>KMDF 版本 1.1


-   以下方法：
    -   [**WdfCommonBufferCreateWithConfig**](https://msdn.microsoft.com/library/windows/hardware/ff545805)
    -   [**WdfDmaEnablerGetFragmentLength**](https://msdn.microsoft.com/library/windows/hardware/ff546986)
    -   [**WdfDmaEnablerWdmGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff547020)

## <a name="kmdf-version-10"></a>KMDF 版本 1.0


初始版本。

 

 





