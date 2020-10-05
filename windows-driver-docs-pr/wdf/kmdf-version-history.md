---
title: KMDF 版本历史记录
description: 本主题列出了 (KMDF) 的内核模式驱动程序框架版本、相应版本的 Windows 操作系统以及在每个版本中所做的更改。
ms.assetid: b920937c-2e5d-48cc-81b5-1462f5d03d75
keywords:
- 内核模式驱动程序 WDK KMDF、修订历史记录
- KMDF WDK，修订历史记录
- 内核模式驱动程序框架 WDK，修订历史记录
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1e31a4e5160c09f327d0f3db4ca5e01606128925
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734317"
---
# <a name="kmdf-version-history"></a>KMDF 版本历史记录


本主题列出了 (KMDF) 的内核模式驱动程序框架版本、相应版本的 Windows 操作系统以及在每个版本中所做的更改。

下表显示了 KMDF 库的发行历史记录：

|KMDF 版本|Release 方法|包含在此版本的 Windows 中|使用的驱动程序运行于|
|--- |--- |--- |--- |
|1.31|Windows 10，版本 2004 WDK|Windows 10 版本 2004 (2020 更新、Vibranium) |Windows 10 版本2004及更高版本|
|1.29|在 WDK 中未发布|Windows 10 版本 1903 (三月2019更新，19H1) |Windows 10 版本 1903 及更高版本|
|1.27|Windows 10，版本 1809 WDK|Windows 10 版本 1809 (2018 更新，Redstone 5) |Windows 10 版本1809及更高版本|
|1.25|Windows 10，版本 1803 WDK|Windows 10 版本 1803 (2018 更新，Redstone 4) |Windows 10 版本 1803 及更高版本|
|1.23|Windows 10，版本 1709 WDK|Windows 10 版本 1709 (秋季创意者更新，Redstone 3) |Windows 10 版本 1709 和更高版本|
|1.21|Windows 10，版本 1703 WDK|Windows 10 版本 1703 (创意者更新，Redstone 2) |Windows 10 版本 1703 及更高版本|
|1.19|Windows 10，版本 1607 WDK|Windows 10 版本 1607 (周年更新，Redstone 1) |Windows 10 版本1607、Windows Server 2016 和更高版本|
|1.17|Windows 10，版本 1511 WDK|Windows 10 版本 1511 (11 月更新，阈值 2) |Windows 10 版本1511、Windows Server 2016 和更高版本|
|1.15|Windows 10 WDK|Windows 10，版本 1507 (阈值 1) |Windows 10，版本1507，Windows Server 2016 及更高版本|
|1.13|Windows 8.1 WDK|Windows 8.1|Windows 8.1 及更高版本|
|1.11|Windows 8 WDK|Windows 8|Windows Vista 及更高版本|
|1.9|Windows 7 WDK|Windows 7|Windows XP 及更高版本|
|1.7|Windows Server 2008 WDK|Windows Vista Service Pack 1 (SP1) 、Windows Server 2008|Windows 2000 及更高版本|
|1.5|Windows Vista WDK|Windows Vista|Windows 2000 及更高版本|
|1.1|仅下载|无|Windows 2000 及更高版本|
|1.0|仅下载|无|Windows XP 及更高版本|

可以将 Windows 驱动程序工具包与 Microsoft Visual Studio 2017 (WDK) 一起使用，以生成在 Windows 7 和更高版本上运行的驱动程序。

若要帮助确定要使用的 WDF 版本，请参阅 [应该使用哪种 framework 版本？](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)。

有关回调和方法的完整列表，以及它们适用于哪些框架和版本，请参阅 [WDF 回调和方法摘要](/windows-hardware/drivers/ddi/_wdf/)。

有关 Windows 10 中 KMDF 驱动程序的新增功能的信息，请参阅 [WDF 驱动程序的新增](index.md)功能。

## <a name="kmdf-version-131"></a>KMDF 版本1.31

* 添加了新的 API [ **WdfDeviceSetDeviceInterfaceStateEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdeviceinterfacestateex)
* 改进现有 API [ **WdfDeviceGetSystemPowerAction**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetsystempoweraction)
* 添加了新的 API [ **WdfPdoInitRemovePowerDependencyOnParent**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitremovepowerdependencyonparent)
* [导向式电源管理框架简介](../kernel/introduction-to-the-directed-power-management-framework.md)

## <a name="kmdf-version-129"></a>KMDF 版本1.29

与版本1.25 不相同。

## <a name="kmdf-version-127"></a>KMDF 版本1.27

与版本1.25 不相同。

## <a name="kmdf-version-125"></a>KMDF 版本1.25

* [为多个版本的 Windows 构建 WDF 驱动程序](building-a-wdf-driver-for-multiple-versions-of-windows.md)

## <a name="kmdf-version-123"></a>KMDF 版本1.23

* 随附功能仅供内部使用。  对于新的 DDIs，请参阅 [WDF 回调和方法摘要](/windows-hardware/drivers/ddi/_wdf/)。

## <a name="kmdf-version-121"></a>KMDF 版本1.21

* [**WdfFileObjectGetInitiatorProcessId**](/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetinitiatorprocessid) 以前仅提供了 UMDF，现已在 KMDF 中提供。
* [**WdfRequestGetRequestorProcessId**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestorprocessid) 以前仅提供了 UMDF，现已在 KMDF 中提供。
* [**WdfObjectDereferenceActual**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)： *文件* 参数类型已从 PCHAR 更改为 PCCH。
* [**WdfObjectReferenceActual**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual)： *文件* 参数类型已从 PCHAR 更改为 PCCH。

## <a name="kmdf-version-119"></a>KMDF 版本1.19

* 添加的[ **WdfDmaTransactionSetSingleTransferRequirement**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement)
* 已在[**WDF_DMA_ENABLER_CONFIG_FLAGS**](/windows-hardware/drivers/ddi/wdfdmaenabler/ne-wdfdmaenabler-_wdf_dma_enabler_config_flags)中添加**WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**标志
* 添加了**STATUS_WDF_TOO_MANY_TRANSFERS** [**WdfDmaTransactionInitialize**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)和[**WdfDmaTransactionDmaCompleted**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)的返回值
* 已将单个传输输出的输出消息添加到 [**！ wdfkd. wdfdmatransaction**](../debugger/-wdfkd-wdfdmatransaction.md) 和 [**！ wdfkd。 wdfdmaenabler**](../debugger/-wdfkd-wdfdmaenabler.md)
* 有关单个传输 DMA 的详细信息，请参阅 [使用单个传输 dma](using-single-transfer-dma.md)。

## <a name="kmdf-version-115"></a>KMDF 版本1.15

-   使用新的 [**WdfDeviceOpenDevicemapKey**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopendevicemapkey) 方法，驱动程序可以访问 **HKEY \_ 本地 \_ 计算机 \\ 硬件 \\ DEVICEMAP**下的子项和值。

## <a name="kmdf-version-113"></a>KMDF 版本1.13


KMDF 版本1.13 添加了以下功能：

-   将 **CanWakeDevice** 成员添加到 [**WDF \_ 中断 \_ 配置**](/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config) 结构，以支持可用于将设备从低功耗 Dx 状态恢复为完全打开的 D0 状态的中断。 有关详细信息，请参阅 [使用中断唤醒设备](using-an-interrupt-to-wake-a-device.md)。
-   支持高分辨率计时器。 有关详细信息，请参阅 [使用计时器](using-timers.md)。
-   支持在系统处于低功耗状态时，不会唤醒系统的计时器。 有关详细信息，请参阅 [使用计时器](using-timers.md)。
-   [访问统一设备属性模型](accessing-the-unified-device-property-model.md)中所述的以下 KMDF/UMDF 方法：
    -   [**WdfDeviceAllocAndQueryPropertyEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
    -   [**WdfDeviceAssignProperty**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
    -   [**WdfDeviceInitSetIoTypeEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)
    -   [**WdfDeviceQueryPropertyEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
    -   [**WdfFdoInitQueryPropertyEx**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

有关 UMDF 版本的信息，请参阅 [Umdf 版本历史记录](umdf-version-history.md)。

## <a name="kmdf-version-111"></a>KMDF 版本1.11


版本1.11 添加了以下功能：

-   [系统模式 DMA](supporting-system-mode-dma.md)

-   支持 [被动级别中断](supporting-passive-level-interrupts.md)

-   单个设备中多个组件的[功能电源状态](supporting-functional-power-states.md)

-   [将 IRP 调度到 I/O 队列](dispatching-irps-to-i-o-queues.md)
-   以下方法：
    -   [**WdfDeviceConfigureWdmIrpDispatchCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)
    -   [**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)
    -   [**WdfDeviceInitSetRemoveLockOptions**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions)
    -   [**WdfDeviceWdmDispatchIrp**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)
    -   [**WdfDmaEnablerConfigureSystemProfile**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile)
    -   [**WdfDmaTransactionAllocateResources**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)
    -   [**WdfDmaTransactionCancel**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)
    -   [**WdfDmaTransactionFreeResources**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources)
    -   [**WdfDmaTransactionGetTransferInfo**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongettransferinfo)
    -   [**WdfDmaTransactionInitializeUsingOffset**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset)
    -   [**WdfDmaTransactionSetChannelConfigurationCallback**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetchannelconfigurationcallback)
    -   [**WdfDmaTransactionSetDeviceAddressOffset**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetdeviceaddressoffset)
    -   [**WdfDmaTransactionSetImmediateExecution**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetimmediateexecution)
    -   [**WdfDmaTransactionSetTransferCompleteCallback**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsettransfercompletecallback)
    -   [**WdfDmaTransactionWdmGetTransferContext**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionwdmgettransfercontext)
    -   [**WdfInterruptQueueWorkItemForIsr**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)
    -   [**WdfInterruptReportActive**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportactive)
    -   [**WdfInterruptReportInactive**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)
    -   [**WdfInterruptTryToAcquireLock**](/previous-versions/hh439284(v=vs.85))
    -   [**WdfIoQueueStopAndPurge**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurge)
    -   [**WdfIoQueueStopAndPurgeSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)
    -   [**WdfIoTargetPurge**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)
    -   [**WdfUsbTargetDeviceCreateIsochUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)
    -   [**WdfUsbTargetDeviceCreateUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)
    -   [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)
    -   [**WdfUsbTargetDeviceQueryUsbCapability**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)
-   添加了 [*EvtDeviceUsageNotificationEx*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification_ex)。

-   将 **IdleTimeoutType** 和 **ExcludeD3Cold** 成员添加到 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)。

-   已将 **ReportInactiveOnPowerDown** 成员添加到 [**WDF \_ 中断 \_ 配置**](/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)。

-   将 **WdfIoTargetPurged** 值添加到 [**WDF \_ IO \_ TARGET \_ 状态**](/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)。

-   将 **WdfSpecialFileBoot** 值添加到 [**WDF \_ 特殊 \_ 文件 \_ 类型**](/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_special_file_type)。

-   已将 **DbgWaitForSignalTimeoutInSec** 添加到 [用于调试基于框架的驱动程序的注册表值](registry-values-for-debugging-kmdf-drivers.md)。

-   添加了 [InstallWdf](/samples/browse/)、 [MultiComp](/samples/browse/)和 [SingleComp](/samples/browse/) 示例。

## <a name="kmdf-version-19"></a>KMDF 版本1。9


版本1.9 添加了以下功能：

-   I/o 队列的[保证前进进度](guaranteeing-forward-progress-of-i-o-operations.md)

-   支持从子设备的 i/o 队列到父设备的 i/o 队列的[正在重新排队 i/o 请求](requeuing-i-o-requests.md)

-   能够为单独的队列对象指定 [队列级别的同步](/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_synchronization_scope) 。

-   以下方法：
    -   [**WdfDeviceGetSystemPowerAction**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetsystempoweraction)
    -   [**WdfDeviceRemoveDependentUsageDeviceObject**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceremovedependentusagedeviceobject)
    -   [**WdfInterruptSetExtendedPolicy**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsetextendedpolicy)
    -   [**WdfPdoInitAllowForwardingRequestToParent**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent)
    -   [**WdfPdoInitAssignContainerID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigncontainerid)
    -   [**WdfPreDeviceInstallEx**](/windows-hardware/drivers/ddi/wdfinstaller/nf-wdfinstaller-wdfpredeviceinstallex)
    -   [**WdfRequestForwardToParentDeviceIoQueue**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoparentdeviceioqueue)
    -   [**WdfRequestMarkCancelableEx**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)
-   将 **NumberOfPresentedRequests** 成员添加到 [**WDF \_ IO \_ 队列 \_ CONFIG**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config) 结构，以便驱动程序可以限制该框架从并行 i/o 队列传递到驱动程序的 i/o 请求数。

-   已将 **WdfFileObjectCanBeOptional** 标志添加到 [**WDF \_ FILEOBJECT \_ 类**](/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_fileobject_class) 结构。

-   将 **TolerableDelay** 成员添加到 [**WDF \_ 计时器 \_ 配置**](/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config) 结构。

-   添加了 [WdfDefaultIdleInWorkingState 和 WdfDefaultWakeFromSleepState](user-control-of-device-idle-and-wake-behavior.md) 注册表值。

## <a name="kmdf-version-17"></a>KMDF 版本1。7


-   可以[**WdfDeviceEnqueueRequest**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)在 IRQL &lt; = 调度级别调用 WdfDeviceEnqueueRequest 方法 \_ 。

-   如果指定的工作项已在工作项队列上，则可以调用 [**WdfWorkItemEnqueue**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue) 方法。

-   添加了 [*EvtDeviceArmWakeFromSxWithReason*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason) 事件回调函数。

-   将 **ArmForWakeIfChildrenAreArmedForWake** 和 **IndicateChildWakeOnParentWake** 成员添加到 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 唤醒 \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings) 结构中。

## <a name="kmdf-version-15"></a>KMDF 版本1。5


-   [**WdfUsbInterfaceGetNumSettings**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumsettings)

-   已将 **DriverPoolTag** 成员添加到 [**WDF \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)。

## <a name="kmdf-version-11"></a>KMDF 版本1。1


-   以下方法：
    -   [**WdfCommonBufferCreateWithConfig**](/windows-hardware/drivers/ddi/wdfcommonbuffer/nf-wdfcommonbuffer-wdfcommonbuffercreatewithconfig)
    -   [**WdfDmaEnablerGetFragmentLength**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablergetfragmentlength)
    -   [**WdfDmaEnablerWdmGetDmaAdapter**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter)

## <a name="kmdf-version-10"></a>KMDF 版本1。0


初始版本。

