---
title: UMDF 版本历史记录
description: 本主题列出了用户模式驱动程序框架（UMDF）的版本、相应版本的 Windows 操作系统以及在每个版本中所做的更改。
ms.assetid: f3e895c6-6801-4033-adaa-d7d04a46db0a
keywords:
- UMDF WDK，修订历史记录
- UMDF WDK，版本信息
- 修订历史记录 WDK UMDF
- 版本信息 WDK UMDF
ms.date: 03/29/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0b2d6925905add88771007370104055068b96d80
ms.sourcegitcommit: 677a9aeb3fb0c29fd8984f271fd803f15182fdb2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80226526"
---
# <a name="umdf-version-history"></a>UMDF 版本历史记录


本主题列出了用户模式驱动程序框架（UMDF）的版本、相应版本的 Windows 操作系统以及在每个版本中所做的更改。

下表显示了 UMDF 库的发行历史记录：

|UMDF 版本|Release 方法|包含在此版本的 Windows 中|使用它的驱动程序可以在|
|--- |--- |--- |--- |
|2.29|在 WDK 中未发布|Windows 10 版本1903（2019年3月更新，19H1）|Windows 10 版本1903及更高版本|
|2.27|Windows 10，版本 1809 WDK|Windows 10 版本1809（2018年10月更新，Redstone 5）|Windows 10 版本1809及更高版本|
|2.25|Windows 10，版本 1803 WDK|Windows 10 版本1803（2018更新，Redstone 4）|Windows 10 版本1803及更高版本|
|2.23|Windows 10，版本 1709 WDK|Windows 10 版本1709（秋季创建者更新、Redstone 3）|Windows 10 版本1709及更高版本|
|2.21|Windows 10，版本 1703 WDK|Windows 10 版本1703（创意者更新，Redstone 2）|Windows 10 版本1703及更高版本|
|2.19|Windows 10，版本 1607 WDK|Windows 10 版本1607（周年更新，Redstone 1）|Windows 10，版本1607，Windows Server 2016 及更高版本|
|2.17|Windows 10，版本 1511 WDK|Windows 10 版本1511（11月更新，阈值2）|Windows 10，版本1511，Windows Server 2016 及更高版本|
|2.15|Windows 10 WDK|Windows 10 版本1507（阈值1）|Windows 10，版本1507，Windows Server 2016 及更高版本|
|2.0|Windows 驱动程序工具包（WDK）8。1|Windows 8.1|Windows 8.1 及更高版本|
|1.11|Windows 驱动程序工具包（WDK）8|Windows 8|Windows Vista 及更高版本|
|1.9|Windows 7 WDK|Windows 7|Windows XP 及更高版本|
|1.7|Windows Server 2008 WDK|Windows Vista Service Pack 1 （SP1）、Windows Server 2008|Windows XP 及更高版本|
|1.5|Windows Vista WDK|Windows Vista|Windows XP 及更高版本|


可以将 Windows 驱动程序工具包（WDK）与 Microsoft Visual Studio 2017 一起使用，以生成在 Windows 7 和更高版本上运行的驱动程序。

若要帮助确定要使用的 WDF 版本，请参阅[应该使用哪种 framework 版本？](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)。

有关 Windows 10 中的 UMDF 驱动程序的新增功能的信息，请参阅[WDF 驱动程序的新增](index.md)功能。

## <a name="umdf-version-229"></a>UMDF 版本2.29

与版本2.27 不相同。

## <a name="umdf-version-227"></a>UMDF 版本2.27

* 添加了新 API [**WdfDriverRetrieveDriverDataDirectoryString**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring)

## <a name="umdf-version-225"></a>UMDF 版本2.25

* [针对多个 Windows 版本生成 WDF 驱动程序](building-a-wdf-driver-for-multiple-versions-of-windows.md)
* [**WdfDeviceRetrieveDeviceDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring)

## <a name="umdf-version-223"></a>UMDF 版本2.23

* 随附功能仅供内部使用。  对于新的 DDIs，请参阅[WDF 回调和方法摘要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)。

## <a name="umdf-version-221"></a>UMDF 版本2.21

* [**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)：*文件*参数类型已从 PCHAR 更改为 PCCH。
* [**WdfObjectReferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual)：*文件*参数类型已从 PCHAR 更改为 PCCH。

## <a name="umdf-version-219"></a>UMDF 版本2.19

UMDF 版本2.19 没有更改或添加。

## <a name="umdf-version-217"></a>UMDF 版本2.17

此版本为以下现有接口添加了 UMDF 支持：

-   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)
-   [*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)
-   [**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)
-   [**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)

有关详细信息，请参阅[将 Irp 调度到 I/o 队列](dispatching-irps-to-i-o-queues.md)。

## <a name="umdf-version-215"></a>UMDF 版本2.15

下面是版本2.15 的已更新 DDIs 列表：

-   使用新的[**WdfDeviceOpenDevicemapKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopendevicemapkey)方法，驱动程序可以访问**HKEY\_本地\_计算机\\硬件\\DEVICEMAP**上的子项和值。

-   UMDF 驱动程序可以调用[**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle) ，以便在其堆栈中获取下一个较低内核模式驱动程序的文件句柄。 驱动程序可以将数据写入该句柄，绕过框架用于向本地 i/o 目标发送 i/o 的抽象。

-   UMDF 驱动程序可以请求基础总线驱动程序重新枚举该驱动程序。 请参阅[**WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)。

-   对于具有连接资源的设备，不再需要设置**UmdfDirectHardwareAccess**指令。 请参阅[在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

## <a name="umdf-version-20"></a>UMDF 版本2。0


除了[具有 umdf 的入门](getting-started-with-umdf-version-2.md)中所述的共享功能，umdf 2.0 版还添加了以下内容：

-   支持在系统处于低功耗状态时，不会唤醒系统的计时器。 有关详细信息，请参阅[使用计时器](using-timers.md)。
-   将**CanWakeDevice**成员添加到[**WDF\_中断\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构，以支持可用于将设备从低功耗 Dx 状态恢复为完全开机 D0 状态的中断。 有关详细信息，请参阅[使用中断唤醒设备](using-an-interrupt-to-wake-a-device.md)。
-   用于 UMDF 驱动程序的单组件单一状态（F0）电源管理。 有关详细信息，请参阅[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)。

-   Wdfkd 中的多个调试器扩展命令现在也可用于 UMDF 2.0 驱动程序。 扩展库还包含用于调试 UMDF 2.0 驱动程序的以下新扩展命令：

    -   [ **!wdfkd.wdfumdevstack**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack)
    -   [ **!wdfkd.wdfumdevstacks**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks)
    -   [ **!wdfkd.wdfumdownirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp)
    -   [ **!wdfkd.wdfumfile**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile)
    -   [ **!wdfkd.wdfumirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp)
    -   [ **!wdfkd.wdfumirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)
    -   [ **!wdfkd.wdfdeviceinterrupts**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts)

    有关扩展命令和框架适用性的列表，请参阅[调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

-   [框架的事件记录器](using-the-framework-s-event-logger.md)或正在进行的*记录器*（IFR）已更新为适用于 UMDF 2.0 驱动程序。
-   其他 WDF 调试器扩展已更新为使用 UMDF 2.0 驱动程序。 有关扩展命令的完整列表，包括适用于哪个框架的信息，请参阅适用于[WDF 驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。
-   已将**WdfIoTargetOpenLocalTargetByFile**添加到[**WDF\_IO\_TARGET\_打开\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_open_type)，以允许 UMDF 驱动程序将驱动程序创建的请求发送到需要关联的文件对象的低级目标。 有关详细信息，请参阅 WDF 的备注 **\_IO\_TARGET\_打开\_类型**。
-   以下仅 UMDF 例程：

    -   [*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)
    -   [**WDF\_IO\_目标\_打开\_参数\_INIT\_\_文件打开\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_open_by_file)
    -   [**WdfDeviceAllocAndQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryinterfaceproperty)
    -   [**WdfDeviceAssignInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigninterfaceproperty)
    -   [**WdfDeviceGetDeviceStackIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestackiotype)
    -   [**WdfDeviceGetHardwareRegisterMappedAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegethardwareregistermappedaddress)
    -   [**WdfDeviceMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)
    -   [**WdfDevicePostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicepostevent)
    -   [**WdfDeviceQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequeryinterfaceproperty)
    -   [**WdfDeviceUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceunmapiospace)
    -   [**WdfFileObjectGetInitiatorProcessId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetinitiatorprocessid) （已添加到 KMDF 1.21）
    -   [**WdfFileObjectGetRelatedFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetrelatedfileobject)
    -   [**WdfRequestGetEffectiveIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgeteffectiveiotype)
    -   [**WdfRequestGetRequestorProcessId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestorprocessid) （已添加到 KMDF 1.21）
    -   [**WdfRequestGetUserModeInitiatedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetusermodedriverinitiatedio)
    -   [**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)
    -   [**WdfRequestIsFromUserModeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver)
    -   [**WdfRequestRetrieveActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)
    -   [**WdfRequestSetActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)
    -   [**WdfRequestSetUserModeDriverInitiatedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetusermodedriverinitiatedio)
-   [访问统一设备属性模型](accessing-the-unified-device-property-model.md)中所述的以下 KMDF/UMDF 方法：

    -   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
    -   [**WdfDeviceAssignProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
    -   [**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)
    -   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
    -   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

    有关详细信息，请参阅[访问统一设备属性模型](accessing-the-unified-device-property-model.md)。

-   支持[**WdfUsbTargetDeviceSelectConfigType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype)中的以下 USB 配置类型：
    -   **WdfUsbTargetDeviceSelectConfigTypeSingleInterface**
    -   **WdfUsbTargetDeviceSelectConfigTypeMultiInterface**
    -   **WdfUsbTargetDeviceSelectConfigTypeInterfacesPairs**
-   支持查询[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)中的以下功能类型：
    -   **GUID\_USB\_功能\_设备\_连接\_高\_速度\_兼容**
    -   **GUID\_USB\_功能\_设备\_连接\_超级\_速度\_兼容**
-   添加了[WDF 寄存器/端口访问函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfhwaccess/)

## <a name="umdf-version-111"></a>UMDF 版本1.11


版本1.11 添加了以下驱动程序提供的回调接口和事件回调函数：

-   [**IPnpCallbackHardware2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware2)

-   [**IPnpCallbackHardwareInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardwareinterrupt)

版本1.11 添加了以下框架提供的接口：

-   [**IWDFCmResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist)

-   [**IWDFDevice3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice3)

-   [**IWDFFile3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile3)

-   [**IWDFInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt)

-   [**IWDFIoRequest3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest3)

-   [**IWDFUnifiedPropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfunifiedpropertystore)

-   [**IWDFUnifiedPropertyStoreFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfunifiedpropertystorefactory)

-   [**IWDFWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfworkitem)

版本1.11 将以下功能添加到基于 UMDF 的驱动程序：

-   [访问硬件和处理中断](accessing-hardware-and-handling-interrupts.md)

-   [在 UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)

-   添加了**UmdfHostProcessSharing**、 **UmdfDirectHardwareAccess**、 **UmdfRegisterAccessMode**、 **UMDFFILEOBJECTPOLICY**和**UMDFFSCONTEXTUSEPOLICY**指令，如在[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)中所述

-   [适用于 UMDF 驱动程序的已知安全标识符（SID）](controlling-device-access.md)

-   统一的属性存储支持，在[基于 UMDF 的驱动程序中使用注册表](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)中所述

-   集成了[**plxntb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer) ，可以使用 UMDF。 在以前的版本中，在对设备句柄进行引用后，此例程会关闭设备对象的句柄。 此行为与 UMDF 不兼容，因为在所有 i/o 都完成后才会发生设备对象上的清理请求。

-   [创建基于 UMDF 的 HID 微型驱动程序](creating-umdf-hid-minidrivers.md)

-   增强了对[支持基于 UMDF 的驱动程序中的空闲电源](supporting-idle-power-down-in-umdf-drivers.md)的支持。 此框架现在可以使设备处于空闲超时期限到期时处于 D3cold 电源状态。 当系统恢复到工作（S0）状态时，框架还可能会导致设备返回到其工作（D0）状态。

-   以下示例是 UMDF 1.11： [WudfVhidmini](https://go.microsoft.com/fwlink/p/?linkid=256226)， [NetNfpProvider](https://go.microsoft.com/fwlink/p/?linkid=256147)中的新示例。

## <a name="umdf-version-19"></a>UMDF 版本1。9


版本1.9 添加了以下驱动程序提供的回调接口：

-   [IPnpCallbackRemoteInterfaceNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackremoteinterfacenotification)

-   [IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

-   [IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

-   [IQueueCallbackIoCanceledOnQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackiocanceledonqueue)

-   [IRemoteInterfaceCallbackEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremoteinterfacecallbackevent)

-   [IRemoteInterfaceCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremoteinterfacecallbackremoval)

-   [IRemoteTargetCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremotetargetcallbackremoval)

-   [IWDFRemoteInterfaceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremoteinterfaceinitialize)

版本1.9 添加了以下框架提供的接口：

-   [IWDFDevice2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice2)

-   [IWDFDeviceInitialize2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize2)

-   [IWDFFile2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile2)

-   [IWDFIoRequest2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest2)

-   [IWDFIoTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget2)

-   [IWDFNamedPropertyStore2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)

-   [IWDFPropertyStoreFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfpropertystorefactory)

-   [IWDFRemoteTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget)

-   [IWDFUsbTargetPipe2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe2)

这些接口将以下功能添加到基于 UMDF 的驱动程序：

-   [远程 i/o 目标](general-i-o-targets-in-umdf.md)

-   [电源策略所有权](power-policy-ownership-in-umdf.md)

-   [直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)缓冲区访问方法

-   USB 设备的[连续读取器](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-pipes-in-umdf-1-x-drivers)

-   增强了对[设备接口](using-device-interfaces-in-umdf-drivers.md)的支持

-   增强了[取消 i/o 请求](canceling-i-o-requests.md)的功能

-   增强了对[注册表](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)的访问权限

 

 





