---
title: UMDF 版本历史记录
description: 本主题列出了版本的用户模式驱动程序框架 (UMDF) 相应版本的 Windows 操作系统，并在每个版本中所做的更改。
ms.assetid: f3e895c6-6801-4033-adaa-d7d04a46db0a
keywords:
- UMDF WDK，修订版本历史记录
- UMDF WDK，版本信息
- 修订版本历史记录 WDK UMDF
- 版本信息 WDK UMDF
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 17972b1697ef1991aac95b549c55261525352b28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372296"
---
# <a name="umdf-version-history"></a>UMDF 版本历史记录


本主题列出了版本的用户模式驱动程序框架 (UMDF) 相应版本的 Windows 操作系统，并在每个版本中所做的更改。

下表显示了 UMDF 库的版本历史记录：

|UMDF 版本|Release 方法|包含在此版本的 Windows|驱动程序使用它可以在上运行|
|--- |--- |--- |--- |
|2.29|不在 WDK 中发布|Windows 10，版本 1903年 （2019 更新，19 H 1 年 3 月）|Windows 10，版本 1903 及更高版本|
|2.27|Windows 10，版本 1809 WDK|Windows 10，版本 1809年 (2018 年 10 月更新 Redstone 5)|Windows 10，版本 1809 及更高版本|
|2.25|Windows 10，版本 1803 WDK|Windows 10，版本 1803年 (2018 年 4 月更新 Redstone 4)|Windows 10，版本 1803 和更高版本|
|2.23|Windows 10 版本 1709 WDK|Windows 10 版本 1709 （Fall Creators Update，Redstone 3）|Windows 10 版本 1709 及更高版本|
|2.21|Windows 10，版本 1703 WDK|Windows 10，版本 1703 （创意者更新，Redstone 2）|Windows 10 版本 1703 及更高版本|
|2.19|Windows 10，版本 1607 WDK|Windows 10，版本 1607 （周年更新，Redstone 1）|Windows 10，版本 1607，Windows Server 2016 及更高版本|
|2.17|Windows 10 版本 1511 WDK|Windows 10 版本 1511 （11 月更新，阈值 2）|Windows 10，版本 1511，Windows Server 2016 及更高版本|
|2.15|Windows 10 WDK|Windows 10 版本 1507 (阈值 1)|Windows 10，版本 1507，Windows Server 2016 及更高版本|
|2.0|Windows 驱动程序工具包 (WDK) 8.1|Windows 8.1|Windows 8.1 及更高版本|
|1.11|Windows 驱动程序工具包 (WDK) 8|Windows 8|Windows Vista 及更高版本|
|1.9|Windows 7 WDK|Windows 7|Windows XP 及更高版本|
|1.7|Windows Server 2008 WDK|Windows Vista Service Pack 1 (SP1)，Windows Server 2008|Windows XP 及更高版本|
|1.5|Windows Vista WDK|Windows Vista|Windows XP 及更高版本|


可以使用 Microsoft Visual Studio 2017 中使用 Windows Driver Kit (WDK) 来构建运行 Windows 7 及更高版本的驱动程序。

确定哪个版本的 WDF 若要使用的帮助，请参阅[应使用哪个框架版本？](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)。

用于 Windows 10 中的 UMDF 驱动程序的新功能的信息，请参阅[What's New for WDF 驱动程序](index.md)。

## <a name="umdf-version-229"></a>UMDF 版本 2.29

从版本 2.27 不变。

## <a name="umdf-version-227"></a>UMDF 版本 2.27

* 添加了新 API [**WdfDriverRetrieveDriverDataDirectoryString**](/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring)

## <a name="umdf-version-225"></a>UMDF 版本 2.25

* [针对多个 Windows 版本生成 WDF 驱动程序](building-a-wdf-driver-for-multiple-versions-of-windows.md)
* [**WdfDeviceRetrieveDeviceDirectoryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring)

## <a name="umdf-version-223"></a>UMDF 版本 2.23

* 仅供内部使用已添加的配套功能。  有关新 DDIs，请参阅[WDF 回调摘要和方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)。

## <a name="umdf-version-221"></a>UMDF 版本 2.21

* [**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdereferenceactual):类型*文件*参数从 PCHAR 更改为 PCCH。
* [**WdfObjectReferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectreferenceactual):类型*文件*参数从 PCHAR 更改为 PCCH。

## <a name="umdf-version-219"></a>UMDF 版本 2.19

没有任何更改或 UMDF 版本 2.19 的新增功能。

## <a name="umdf-version-217"></a>UMDF 版本 2.17

此版本添加了对以下现有接口的 UMDF 支持：

-   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)
-   [*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)
-   [**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)
-   [**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)

有关详细信息，请参阅[调度到的 I/O 队列的 Irp](dispatching-irps-to-i-o-queues.md)。

## <a name="umdf-version-215"></a>UMDF 版本 2.15

下面是更新 DDIs 2.15 版本的列表：

-   新[ **WdfDeviceOpenDevicemapKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceopendevicemapkey)方法允许驱动程序添加到访问子项和值下**HKEY\_本地\_机\\硬件\\DEVICEMAP**。

-   UMDF 驱动程序可以调用[ **WdfIoTargetWdmGetTargetFileHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)若要获取其堆栈中的下一步低内核模式驱动程序的文件句柄。 该驱动程序可以将数据写入该句柄，从而绕过将 I/O 发送到本地的 I/O 目标框架的抽象。

-   UMDF 驱动程序可以请求基础总线驱动程序重新枚举它。 请参阅[ **WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)。

-   设置**UmdfDirectHardwareAccess**指令不再始终是必需的设备的已连接资源。 请参阅[在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

## <a name="umdf-version-20"></a>UMDF 版本 2.0


除了共享功能中所述[入门 UMDF](getting-started-with-umdf-version-2.md)，UMDF 版本 2.0 添加：

-   如果在过期时系统处于低功耗状态无法唤醒系统计时器的支持。 有关详细信息，请参阅[使用计时器](using-timers.md)。
-   添加**CanWakeDevice**成员添加到[ **WDF\_中断\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构，以支持可用于将从设备的中断恢复到其完全处于 D0 状态低功耗 Dx 状态。 有关详细信息，请参阅[中断用于唤醒设备](using-an-interrupt-to-wake-a-device.md)。
-   单组件、 单状态 (F0) 的电源管理 UMDF 驱动程序。 有关详细信息，请参阅[ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)。

-   多个调试器扩展命令中 Wdfkd.dll 现在用于 UMDF 2.0 驱动程序。 扩展插件库还包含专门用于调试 UMDF 2.0 驱动程序的以下新扩展命令：

    -   [ **!wdfkd.wdfumdevstack**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack)
    -   [ **!wdfkd.wdfumdevstacks**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks)
    -   [ **!wdfkd.wdfumdownirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp)
    -   [ **!wdfkd.wdfumfile**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile)
    -   [ **!wdfkd.wdfumirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp)
    -   [ **!wdfkd.wdfumirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)
    -   [ **!wdfkd.wdfdeviceinterrupts**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts)

    扩展命令和 framework 适用性的列表，请参阅[调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

-   [框架的事件记录器](using-the-framework-s-event-logger.md)，或*正在进行录制器*(IFR) 已更新为适用于 UMDF 2.0 驱动程序。
-   已更新其他 WDF 调试器扩展以使用 UMDF 2.0 驱动程序。 有关扩展命令，其中包括有关哪些的将应用于哪个框架，请参阅的信息的完整列表[WDF 驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。
-   添加**WdfIoTargetOpenLocalTargetByFile**到[ **WDF\_IO\_目标\_打开\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_open_type)允许 UMDF若要发送驱动程序创建请求，以降低需要关联的文件对象的目标的驱动程序。 有关详细信息，请参阅的备注**WDF\_IO\_目标\_打开\_类型**。
-   下面的仅限 UMDF 的例程：

    -   [*EvtRequestImpersonate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)
    -   [**WDF\_IO\_TARGET\_OPEN\_PARAMS\_INIT\_OPEN\_BY\_FILE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_open_by_file)
    -   [**WdfDeviceAllocAndQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryinterfaceproperty)
    -   [**WdfDeviceAssignInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigninterfaceproperty)
    -   [**WdfDeviceGetDeviceStackIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestackiotype)
    -   [**WdfDeviceGetHardwareRegisterMappedAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegethardwareregistermappedaddress)
    -   [**WdfDeviceMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicemapiospace)
    -   [**WdfDevicePostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicepostevent)
    -   [**WdfDeviceQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequeryinterfaceproperty)
    -   [**WdfDeviceUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceunmapiospace)
    -   [**WdfFileObjectGetInitiatorProcessId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/nf-wdffileobject-wdffileobjectgetinitiatorprocessid) （添加到 KMDF 1.21）
    -   [**WdfFileObjectGetRelatedFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/nf-wdffileobject-wdffileobjectgetrelatedfileobject)
    -   [**WdfRequestGetEffectiveIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgeteffectiveiotype)
    -   [**WdfRequestGetRequestorProcessId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetrequestorprocessid) （添加到 KMDF 1.21）
    -   [**WdfRequestGetUserModeInitiatedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetusermodedriverinitiatedio)
    -   [**WdfRequestImpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)
    -   [**WdfRequestIsFromUserModeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver)
    -   [**WdfRequestRetrieveActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)
    -   [**WdfRequestSetActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)
    -   [**WdfRequestSetUserModeDriverInitiatedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetusermodedriverinitiatedio)
-   以下 KMDF/UMDF 方法中所述[访问统一的设备属性模型](accessing-the-unified-device-property-model.md):

    -   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
    -   [**WdfDeviceAssignProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
    -   [**WdfDeviceInitSetIoTypeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)
    -   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)
    -   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
    -   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

    有关详细信息，请参阅[访问统一的设备属性模型](accessing-the-unified-device-property-model.md)。

-   中的以下 USB 配置类型的支持[ **WdfUsbTargetDeviceSelectConfigType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ne-wdfusb-_wdfusbtargetdeviceselectconfigtype):
    -   **WdfUsbTargetDeviceSelectConfigTypeSingleInterface**
    -   **WdfUsbTargetDeviceSelectConfigTypeMultiInterface**
    -   **WdfUsbTargetDeviceSelectConfigTypeInterfacesPairs**
-   查询中的以下功能类型的支持[ **WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability):
    -   **GUID\_USB\_功能\_设备\_连接\_高\_速度\_兼容**
    -   **GUID\_USB\_功能\_设备\_连接\_超级\_速度\_兼容**
-   添加[WDF 注册/端口访问函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfhwaccess/)

## <a name="umdf-version-111"></a>UMDF 版本 1.11


1\.11 版新增了以下驱动程序提供的回调接口和事件的回调函数：

-   [**IPnpCallbackHardware2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware2)

-   [**IPnpCallbackHardwareInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardwareinterrupt)

版本 1.11 添加框架提供了以下接口：

-   [**IWDFCmResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfcmresourcelist)

-   [**IWDFDevice3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice3)

-   [**IWDFFile3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile3)

-   [**IWDFInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfinterrupt)

-   [**IWDFIoRequest3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest3)

-   [**IWDFUnifiedPropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfunifiedpropertystore)

-   [**IWDFUnifiedPropertyStoreFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfunifiedpropertystorefactory)

-   [**IWDFWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfworkitem)

版本 1.11 基于 UMDF 驱动程序添加了以下功能：

-   [访问硬件和处理中断](accessing-hardware-and-handling-interrupts.md)

-   [使用设备池在 UMDF 驱动程序](using-device-pooling-in-umdf-drivers.md)

-   添加**UmdfHostProcessSharing**， **UmdfDirectHardwareAccess**， **UmdfRegisterAccessMode**， **UmdfFileObjectPolicy**，和**UmdfFsContextUsePolicy**中所述的指令[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)

-   [UMDF 驱动程序的已知安全标识符 (SID)](controlling-device-access.md)

-   统一中所描述的属性存储区支持[使用的注册表中基于 UMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)

-   [**IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)集成来使用 UMDF。 在以前版本中，此例程将使设备的句柄的引用后关闭设备对象的句柄。 此行为是所有 i/o 操作完成后，设备对象上的清除请求不会发生之前的 UMDF 的假定条件下不兼容。

-   [创建基于 UMDF 的 HID 微型驱动程序](creating-umdf-hid-minidrivers.md)

-   对增强的支持[支持空闲电源关闭基于 UMDF 驱动程序中](supporting-idle-power-down-in-umdf-drivers.md)。 当空闲超时时间到期时，框架现在可以在 D3cold 电源状态将设备。 该框架也会导致设备后，系统将恢复为其工作 (S0) 状态时返回到其工作 (D0) 状态。

-   下面的示例是 UMDF 1.11 中的新增功能：[WudfVhidmini](https://go.microsoft.com/fwlink/p/?linkid=256226)， [NetNfpProvider](https://go.microsoft.com/fwlink/p/?linkid=256147)。

## <a name="umdf-version-19"></a>UMDF 1.9 版


1\.9 版中添加以下驱动程序提供的回调接口：

-   [IPnpCallbackRemoteInterfaceNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackremoteinterfacenotification)

-   [IPowerPolicyCallbackWakeFromS0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

-   [IPowerPolicyCallbackWakeFromSx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

-   [IQueueCallbackIoCanceledOnQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackiocanceledonqueue)

-   [IRemoteInterfaceCallbackEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremoteinterfacecallbackevent)

-   [IRemoteInterfaceCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremoteinterfacecallbackremoval)

-   [IRemoteTargetCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremotetargetcallbackremoval)

-   [IWDFRemoteInterfaceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfremoteinterfaceinitialize)

版本 1.9 添加框架提供了以下接口：

-   [IWDFDevice2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice2)

-   [IWDFDeviceInitialize2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize2)

-   [IWDFFile2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile2)

-   [IWDFIoRequest2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest2)

-   [IWDFIoTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget2)

-   [IWDFNamedPropertyStore2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore2)

-   [IWDFPropertyStoreFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfpropertystorefactory)

-   [IWDFRemoteTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfremotetarget)

-   [IWDFUsbTargetPipe2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe2)

这些接口将添加到基于 UMDF 驱动程序的以下功能：

-   [远程 I/O 目标](general-i-o-targets-in-umdf.md)

-   [电源策略所有权](power-policy-ownership-in-umdf.md)

-   [直接 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)缓冲访问方法

-   [持续读取器](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-pipes-in-umdf-1-x-drivers)的 USB 设备

-   增强了对支持[设备接口](using-device-interfaces-in-umdf-drivers.md)

-   增强的能力[取消 I/O 请求](canceling-i-o-requests.md)

-   增强对访问[注册表](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)

 

 





