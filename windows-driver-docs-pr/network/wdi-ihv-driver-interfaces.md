---
title: WDI IHV 驱动程序接口
description: WDI IHV 微型端口就像任何其他 NDIS 微型端口驱动程序，并且将采用的开发实践和任何 NDIS 微型端口的文档。
ms.assetid: B4528C70-9FE4-4E00-9D0B-8832CCEC982E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cd10bc2af08445689c1ffd96bda3598b567c13a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385626"
---
# <a name="wdi-ihv-driver-interfaces"></a>WDI IHV 驱动程序接口


WDI IHV 微型端口就像任何其他 NDIS 微型端口驱动程序，并且将采用的开发实践和任何 NDIS 微型端口的文档。 MS 组件和 WDI IHV 驱动程序之间拆分 NDIS 处理程序的本机 WLAN 微型端口驱动程序的职责。 Microsoft WLAN 组件负责的 NDIS 要求适用于所有的 Wi-fi 微型端口，以便每个 IHV 不必重做所有此项工作。 如下所述的映射和本机 WLAN IHV 微型端口时应用到 WDI IHV 微型端口的 NDIS 处理程序的行为更改。

-   [驱动程序安装](#driver-installation)
-   [DriverEntry](#driverentry)
-   [MiniportSetOptions](#miniportsetoptions)
-   [MiniportInitializeEx](#miniportinitializeex)
-   [MiniportHaltEx](#miniporthaltex)
-   [MiniportDriverUnload](#miniportdriverunload)
-   [MiniportPause](#miniportpause)
-   [MiniportRestart](#miniportrestart)
-   [MiniportResetEx](#miniportresetex)
-   [MiniportDevicePnPEventNotify](#miniportdevicepnpeventnotify)
-   [MiniportShutdownEx](#miniportshutdownex)
-   [MiniportOidRequest](#miniportoidrequest)
-   [MiniportCancelOidRequest](#miniportcanceloidrequest)
-   [NdisMIndicateStatusEx](#ndismindicatestatusex)
-   [MiniportDirectOidRequest](#miniportdirectoidrequest)
-   [MiniportCancelDirectOidRequest](#miniportcanceldirectoidrequest)
-   [MiniportSendNetBufferLists](#miniportsendnetbufferlists)
-   [MiniportCancelSend](#miniportcancelsend)
-   [MiniportReturnNetBufferLists](#miniportreturnnetbufferlists)
-   [WDI 处理程序：MiniportWdiOpenAdapter](#wdi-handler-miniportwdiopenadapter)
-   [WDI 处理程序：MiniportWdiCloseAdapter](#wdi-handler-miniportwdicloseadapter)

## <a name="driver-installation"></a>驱动程序安装


没有到 WDI IHV 微型端口驱动程序加载并在系统上安装的方式的更改。 类似于 IHV 本机 WLAN 微型端口驱动程序的 INF 和安装过程。 现有的 NDIS 驱动程序，如当 IHV 驱动程序需要加载以使用 IHV WLAN 适配器，操作系统将调用 IHV 微型端口驱动程序的 DriverEntry 例程。

## <a name="driverentry"></a>DriverEntry


操作系统将直接调用 WDI IHV 微型端口驱动程序的 DriverEntry 例程。 IHV 微型端口遵循大部分的正则 NDIS miniport DriverEntry 例程的指导原则。 一个例外情况是，而不是调用[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)，IHV 微型端口调用[ **NdisMRegisterWdiMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/mt297596)告诉操作系统，使 Microsoft WLAN 组件。

密钥参数如下[ **NdisMRegisterWdiMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/mt297596)。

-   [**NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958):这是本机 Wi-fi 微型端口使用注册到 NDIS 原始 NDIS 结构。 对于 WDI 模型，大部分的处理程序参数是可选的。 唯一所需的处理程序是**微型端口\_OID\_请求\_处理程序**并**微型端口\_驱动程序\_卸载**。 **微型端口\_OID\_请求\_处理程序**用于将 WDI 消息传递给 IHV 驱动程序。 如果指定任何其他处理程序，则 Microsoft WLAN 组件通常调用处理程序后都执行其自己的处理程序处理。
-   [**NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://msdn.microsoft.com/library/windows/hardware/mt297617):这是一组新的 WDI 微型端口驱动程序必须实现的处理程序。 IHV 驱动程序使用它来注册控件路径的附加处理程序和完整集的处理程序的数据路径。

当 IHV 微型端口调用 NdisMRegisterWdiMiniportDriver 时，Microsoft WLAN 组件更新的处理程序[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958) ，并调用的 NDIS [ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)。 更新已完成，以便 Microsoft WLAN 组件可以拦截它可以为其提供协助/简化到 WDI IHV 微型端口驱动程序的处理程序。

下面是 WDI IHV 微型端口驱动程序的 DriverEntry 过程的典型工作流

![wdi driverentry 流](images/wdi-driverentry-flow.png)

DriverEntry 有关详细信息，请参阅[ **DriverEntry 的 NDIS 微型端口驱动程序**](https://msdn.microsoft.com/library/windows/hardware/ff548818)。

## <a name="miniportsetoptions"></a>MiniportSetOptions


如上述 DriverEntry 关系图所示，如果已注册 WDI IHV 微型端口[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)处理程序中，操作系统将调用微型端口驱动程序的上下文中该函数调用[ **NdisMRegisterWdiMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/mt297596)。

如果 IHV 微型端口驱动程序将注册使用的任何选项处理[ **NdisSetOptionalHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff564550)，这些处理程序可能不会序列化通过 WDI 层由 Microsoft 组件。 因此，IHV 组件负责处理这些处理程序的任何同步要求。

## <a name="miniportinitializeex"></a>MiniportInitializeEx


WDI 模型将拆分[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)到多个 WDI 行为接口调用。

1.  调用[ *MiniportWdiAllocateAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297559)。

    当操作系统发现 IHV 硬件的实例时，这是首次调用到 WDI IHV 微型端口驱动程序。 在此调用，WDI 微型端口执行创建的软件表示形式所需的操作 (**MiniportAdapterContext**) 的设备。 它还确定设备要填写的相关信息[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构。 当 Microsoft 组件发送 WDI 命令向下执行特定初始化时，设备的 Wi-fi 堆栈的实际初始化完成更高版本。

    使用从 WDI IHV 微型端口驱动程序中获取数据，Microsoft 组件都会调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)并设置[ **NDIS\_微型端口\_适配器\_注册\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565934) NDIS 上。 大多数字段**NDIS\_微型端口\_适配器\_注册\_属性**将填入由 Microsoft 组件的默认值。 IHV 驱动程序必须填充**MiniportAdapterContext**并**InterfaceType**字段。

    此调用返回后从 IHV 微型端口驱动程序，它会开始接收 WDI 命令通过其[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)处理程序。 在此调用，Microsoft 组件可能无法再执行重置/恢复操作，因此，在此处执行任何活动应快速和可靠。

2.  调用[ *MiniportWdiOpenAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297564)。

    之后[ *MiniportWdiAllocateAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297559)，Microsoft 的组件调用[ *MiniportWdiOpenAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297564)加载固件和初始化硬件。

3.  使用多个 WDI 命令[ *MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)。

    之后[ *MiniportWdiOpenAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297564)，Microsoft 组件将下面的任务/属性/调用发送到 IHV 微型端口。

    1.  调用[ *MiniportWdiTalTxRxInitialize* ](https://msdn.microsoft.com/library/windows/hardware/mt297580)初始化的数据路径并交换处理程序。
    2.  调用[OID\_WDI\_获取\_适配器\_功能](https://msdn.microsoft.com/library/windows/hardware/dn925838)用于获得适配器的功能。
    3.  调用[OID\_WDI\_设置\_适配器\_配置](https://msdn.microsoft.com/library/windows/hardware/dn925853)配置适配器。
    4.  调用[OID\_WDI\_任务\_设置\_单选\_状态](https://msdn.microsoft.com/library/windows/hardware/dn925963)用于设置初始广播的状态，如果它尚未在预期的状态。
    5.  调用[ *MiniportWdiTalTxRxStart* ](https://msdn.microsoft.com/library/windows/hardware/mt297585)若要设置的数据路径。
    6.  调用[OID\_WDI\_任务\_创建\_端口](https://msdn.microsoft.com/library/windows/hardware/dn925949)创建初始端口。

    其他命令还可向下发送到 IHV 组件作为 Microsoft 组件 MiniportInitializeEx 处理的一部分。 但是，直到[ *MiniportWdiStartOperation* ](https://msdn.microsoft.com/library/windows/hardware/mt297575)调用时，需要无线通信的 Microsoft 组件不会向下发送的任何任务。 除[OID\_WDI\_任务\_打开](https://msdn.microsoft.com/library/windows/hardware/dn925954)始终发送的第一次，可能会更改其他命令/调用的顺序。

    使用从 WDI IHV 微型端口驱动程序中获取数据，Microsoft 组件都会调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)并设置[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)并[ **NDIS\_微型端口\_适配器\_本机\_802\_11\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565926) NDIS 上。

4.  调用[ *MiniportWdiStartOperation*](https://msdn.microsoft.com/library/windows/hardware/mt297575)。

    这是一个可选 WDI 微型端口处理程序内的[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://msdn.microsoft.com/library/windows/hardware/mt297617) ，可以使用 IHV 驱动程序执行的任何其他 MiniportInitializeEx 任务。 它还可通过 IHV 微型端口为 Microsoft 组件已初始化的微型端口和微型端口的提示可以启动任何所需的后台活动。

    下图显示了 MiniportInitializeEx 的流。

    ![wdi 微型端口初始化流](images/wdi-miniport-initialization-flow.png)

    如果中间操作失败，Microsoft 组件撤消上一操作和微型端口打开的失败。 例如，如果[OID\_WDI\_任务\_创建\_端口](https://msdn.microsoft.com/library/windows/hardware/dn925949)失败，数据路径已被清除， [OID\_WDI\_任务\_关闭](https://msdn.microsoft.com/library/windows/hardware/dn925947)发送，并且微型端口失败。

## <a name="miniporthaltex"></a>MiniportHaltEx


在本机 Wi-fi 微型端口， [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)用于告知微型端口，以便停止操作并清除适配器实例。 在 WDI 模型中，Microsoft 组件处理原始*MiniportHaltEx*调用，并将它拆分为多个 WDI 接口调用。

1.  调用[ *MiniportWdiStopOperation*](https://msdn.microsoft.com/library/windows/hardware/mt297576)。

    这是一个可选 WDI 微型端口处理程序内的[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://msdn.microsoft.com/library/windows/hardware/mt297617) IHV 驱动程序可用于撤消它在中执行的操作[ *MiniportWdiStartOperation*](https://msdn.microsoft.com/library/windows/hardware/mt297575)。

2.  使用多个 WDI 命令[ *MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)。

    之后[ *MiniportWdiStopOperation*](https://msdn.microsoft.com/library/windows/hardware/mt297576)，Microsoft 组件发送到 IHV 微型端口，以便清理 IHV 驱动程序的当前状态的任务/属性。 此清理可能包括以下内容。

    1.  调用[OID\_WDI\_任务\_断开连接](https://msdn.microsoft.com/library/windows/hardware/dn925951)/[OID\_WDI\_任务\_停止\_AP](https://msdn.microsoft.com/library/windows/hardware/dn925965)关闭任何现有连接。
    2.  调用[OID\_WDI\_任务\_删除\_端口](https://msdn.microsoft.com/library/windows/hardware/dn925950)到删除所有创建的端口。
    3.  调用[ *MiniportWdiTalTxRxStop* ](https://msdn.microsoft.com/library/windows/hardware/mt297586)停止数据路径。
    4.  调用[ *MiniportWdiTalTxRxDeinitialize* ](https://msdn.microsoft.com/library/windows/hardware/mt297578)以 deinitialize 数据路径。
    5.  调用以清理硬件状态。 这发送到 IHV 使用[ *MiniportWdiCloseAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297561) IHV 驱动程序通过已注册的。

3.  上述命令的所有调用的是，Microsoft 组件都会调用[ *MiniportWdiFreeAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297562)让 IHV 驱动程序删除它可能具有的任何软件状态。

下图显示了 MiniportHaltEx 的流。

![wdi 微型端口暂停流](images/wdi-miniport-halt-flow.png)

如果设备已意外删除或系统关闭电源，则不执行 MiniportHaltEx 处理。 有关在意外删除，请参阅[MiniportDevicePnPEventNotify](#miniportdevicepnpeventnotify)处理程序的行为。 有关系统关闭，请参阅[MiniportShutdownEx](#miniportshutdownex)处理程序的行为。

## <a name="miniportdriverunload"></a>MiniportDriverUnload


[*MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)是卸载 WDI IHV 微型端口之前调用的处理程序。 WDI IHV 微型端口驱动程序将调用 Microsoft 组件来取消注册自身。 Microsoft 的组件调用[ **NdisMDeregisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563578)。

下图显示了 MiniportDriverUnload 的流。

![wdi 微型端口驱动程序卸载流](images/wdi-miniport-driver-unload-flow.png)

## <a name="miniportpause"></a>MiniportPause


NDIS [ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)要求将由 Microsoft 组件。 作为 MiniportPause 的一部分，Microsoft 组件停止数据路径，并等待其清理。 WDI IHV 微型端口 （可选） 可以注册以进行[ *MiniportWdiPostAdapterPause* ](https://msdn.microsoft.com/library/windows/hardware/mt297565)后完成的数据路径清理 Microsoft 组件调用的回调。

下图显示了 MiniportPause 的流。

![wdi 微型端口暂停流](images/wdi-miniport-pause-flow.png)

## <a name="miniportrestart"></a>MiniportRestart


NDIS [ *MiniportRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff559435)要求将由 Microsoft 组件。 作为 MiniportRestart 的一部分，Microsoft 组件撤消它的 MiniportPause 一部分执行的数据路径暂停工作。 WDI IHV 微型端口 （可选） 可以注册以进行[ *MiniportWdiPostAdapterRestart* ](https://msdn.microsoft.com/library/windows/hardware/mt297566)完成重新启动的数据路径之后，由 Microsoft 组件调用的回调。

下图显示了 MiniportRestart 的流。

![wdi 微型端口重新启动流](images/wdi-miniport-restart-flow.png)

## <a name="miniportresetex"></a>MiniportResetEx


[*MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)未由 Microsoft 组件。 WDI IHV 微型端口 （可选） 可以注册以进行*MiniportResetEx*由 Microsoft 组件调用的回调。

## <a name="miniportdevicepnpeventnotify"></a>MiniportDevicePnPEventNotify


[*MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)用于通知即插即用事件，例如设备的意外删除的 NDIS 驱动程序。 NDIS 发送此通知，将首先转发到 WDI IHV 微型端口进行处理。 IHV 组件完成处理后后，Microsoft 组件执行适当的处理此事件。 转发到 IHV 组件的调用不序列化与其他任务和回调。

下图显示了 MiniportDevicePnPEventNotify 的流。

![wdi 微型端口驱动器即插即用通知工作流](images/wdi-miniport-device-pnp-notification-flow.png)

## <a name="miniportshutdownex"></a>MiniportShutdownEx


[*MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)用于通知系统关闭事件有关的 NDIS 驱动程序。 当 NDIS 发送此通知时，它首先由 Microsoft 组件处理。 Microsoft 组件完成处理后，它将事件传递给处理 WDI IHV 微型端口。

下图显示了 MiniportShutdownEx 的流。

![wdi 微型端口关闭流](images/wdi-miniport-shutdown-flow.png)

## <a name="miniportoidrequest"></a>MiniportOidRequest


[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)处理程序所需的处理程序必须实现 WDI IHV 微型端口。 Microsoft 组件使用它将 WDI 命令提交到 IHV 微型端口。 它还用于转发的 Microsoft 组件不处理到 IHV 微型端口的 Oid。

[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)调入 WDI IHV 微型端口应视为 WDI 命令 M1 消息。 完成的 OID (无论是通过[ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)或通过不挂起从返回*MiniportOidRequest*) 应被视为 M3 消息WDI 任务/命令。

对于每个 WDI 命令，字段有两个潜在的 NDIS\_操作-中的状态代码可能会返回状态代码[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)调用 (或[ **NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622))，和中的状态代码[ **WDI\_消息\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn926074)字段 (在 OID 完成或通过[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600))。 Microsoft 组件始终会查看 NDIS\_OID 完成后它会查看之前的状态**WDI\_消息\_HEADERStatus**字段。 WDI OID 处理 IHV 组件的预期要求如下所示。

1.  将其提交给 IHV 组件使用 WDI Oid [ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)**RequestType**的**NdisRequestMethod**，并相应的消息和消息长度位于**数据。方法\_INFORMATION.InformationBuffer**和**数据。方法\_信息。InputBufferLength**分别字段。
2.  IHV 组件中报告了错误 OID 完成是否存在错误时正在处理命令，并设置的状态字段[ **WDI\_消息\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn926074)到失败是否 Wi-fi 级故障影响。
3.  有关任务和属性，该请求的端口号处于[ **WDI\_消息\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn926074)**PortId**字段。 **PortNumber**中[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)始终设置为 0。
4.  对于完成 OID 时，它是可接受[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)返回 NDIS\_状态\_PENDING 和更高版本完成 OID （同步或异步）与[ **NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)。
5.  如果 IHV 组件完成与 NDIS OID\_状态\_成功后，它必须填充**BytesWritten**字段具有适当数量的字节数，包括空间的 OID 请求[**WDI\_消息\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn926074)。
6.  如果 IHV 组件不具有足够的空间**数据。方法\_信息。OutputBufferLength**字段以填充响应，完成与 NDIS OID\_状态\_缓冲区\_过\_短，并填充**数据。方法\_信息。BytesNeeded**字段。 Microsoft 组件可能会尝试分配请求的大小的缓冲区并提交对 IHV 的新请求。
7.  如果它是一项任务，任务的 M4 ([**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)) 必须仅表示如果任务已报告为成功-启动 OID 完成已成功和**状态**中[ **WDI\_消息\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn926074) OID 中完成成功。

下图显示了映射到单个 WDI 命令 NDIS OID 请求的示例。 OID 请求提交由操作系统中，Microsoft 组件将其转换为 WDI OID 请求，并将提交到 IHV 微型端口 WDI OID 请求。 IHV 微型端口完成 OID，Microsoft 组件适当地完成原始的 OID 请求。

![wdi 微型端口 oid 请求序列的单个 wdi 命令](images/wdi-miniport-oid-request-single.png)

如果 OriginalOidRequest 映射到多个 WDI OidRequests WDI 请求之一发生故障，OriginalOidRequest 也会失败。 如果一小部分中间操作已完成后，Microsoft 组件尝试撤消支持清理操作。

下图显示了 NDIS OID 请求处理，则由 Microsoft 组件已完成的示例。 当 OID 请求提交的操作系统的 Microsoft 组件进程，并完成 OID。 此 OID 不传递到 WDI IHV 微型端口。

![wdi 微型端口 oid 请求序列的 oid 由 microsoft 组件处理](images/wdi-miniport-oid-request-wdi-handled.png)

不理解的 Microsoft 组件的 Oid 将转发直接到 IHV 组件进行处理。

![wdi 微型端口 oid 请求序列的 oid 未由 microsoft 组件](images/wdi-miniport-oid-request-unknown.png)

MiniportOidRequest 的行为保持不变 （相比于本机 Wi-fi 微型端口） 的 WDI IHV 微型端口驱动程序。 调用进行序列化和 IHV 微型端口可以完成它以同步方式还是以异步方式通过调用[ **NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)。

## <a name="miniportcanceloidrequest"></a>MiniportCancelOidRequest


这是一个可选的处理程序，需要处理未映射到 WDI 消息的 Oid WDI IHV 微型端口使用。 此处理程序不用于任何 WDI Oid。 WDI Oid 必须快速完成，并且没有要尝试取消挂起的 OID 的 IHV 微型端口驱动程序不需要。 WDI 任务取消使用适当的取消任务 OID 请求进行处理。 对于未映射的 Oid NDIS 被定义预期的行为。

## <a name="ndismindicatestatusex"></a>NdisMIndicateStatusEx


[**NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600) WDI IHV 微型端口用于将指示发送至 Microsoft 组件。 指示可能未经请求的指示，如 TKIP MIC 失败或请求任务的完成 (M4) 的指示。

下图显示了具有相应的 NDIS/本机 Wi-fi 指示的 WDI 指示的示例。 指示通过提交时对 Microsoft 组件 IHV 微型端口，Microsoft 组件将其转换为现有表示，并将其转发到操作系统。

![wdi 微型端口状态指示流](images/wdi-miniport-status-indication-flow.png)

下图显示了具有没有相应的 NDIS/本机 Wi-fi 指示的 WDI 指示的示例。 这是由 Microsoft 组件进行处理。

![而不直接映射到 ndis wdi 状态指示](images/wdi-miniport-status-indication-not-ndis.png)

下图显示了由 Microsoft 组件无法识别的指示。 作为转发所指示的是操作系统。

![wdi 状态指示无法识别的 microsoft 组件](images/wdi-miniport-status-indication-unknown.png)

NdisMIndicateStatusEx 的行为保持不变 （相比于本机 Wi-fi 微型端口） 的 WDI IHV 微型端口驱动程序。

## <a name="miniportdirectoidrequest"></a>MiniportDirectOidRequest


这是一个可选处理程序，如果它需要处理未映射到 WDI 消息的直接 Oid 由 WDI IHV 微型端口驱动程序注册。 为 Wi-Fi Direct 的所有现有直接 Oid 将映射到 WDI 消息，因此不需要进行此处理程序来支持该功能。 不支持直接 Oid 由 Microsoft 组件不会序列化。

## <a name="miniportcanceldirectoidrequest"></a>MiniportCancelDirectOidRequest


这是一个可选的处理程序，需要处理未映射到 WDI 消息的直接 Oid WDI IHV 微型端口使用。 对于未映射的 Oid NDIS 被定义预期的行为。

## <a name="miniportsendnetbufferlists"></a>MiniportSendNetBufferLists


此处理程序不使用 WDI IHV 微型端口驱动程序中，不应提供。 Microsoft 组件使用的数据路径处理程序通过注册[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://msdn.microsoft.com/library/windows/hardware/mt297617)到提交到 IHV 微型端口发送数据包。

## <a name="miniportcancelsend"></a>MiniportCancelSend


此处理程序不使用 WDI IHV 微型端口驱动程序中，不应提供。

## <a name="miniportreturnnetbufferlists"></a>MiniportReturnNetBufferLists


此处理程序不使用 WDI IHV 微型端口驱动程序中，不应提供。 Microsoft 组件使用的数据路径处理程序通过注册[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://msdn.microsoft.com/library/windows/hardware/mt297617)到返回到 IHV 微型端口接收到的数据包。

## <a name="wdi-handler-miniportwdiopenadapter"></a>WDI 处理程序：MiniportWdiOpenAdapter


[ *MiniportWdiOpenAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297564) Microsoft 组件使用处理程序以启动 IHV 驱动程序打开的任务操作。 此调用必须快速完成，并且如果打开操作已成功启动，IHV 必须返回 NDIS\_状态\_在此调用和调用的成功[ **OpenAdapterComplete** ](https://msdn.microsoft.com/library/windows/hardware/mt297602)处理程序传递到[ **NDIS\_WDI\_INIT\_参数**](https://msdn.microsoft.com/library/windows/hardware/mt297621)参数[ *MiniportWdiAllocateAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297559)。

## <a name="wdi-handler-miniportwdicloseadapter"></a>WDI 处理程序：MiniportWdiCloseAdapter


[ *MiniportWdiCloseAdapter* ](https://msdn.microsoft.com/library/windows/hardware/mt297561) Microsoft 组件使用处理程序以启动 IHV 驱动程序上的关闭任务操作。 此调用必须快速完成，并且如果打开操作已成功启动，IHV 必须返回 NDIS\_状态\_在此调用和调用的成功[ **CloseAdapterComplete** ](https://msdn.microsoft.com/library/windows/hardware/mt297598)处理程序传递到[ **NDIS\_WDI\_INIT\_参数**](https://msdn.microsoft.com/library/windows/hardware/mt297621)参数[ *MiniportWdiAllocateAdapter*](https://msdn.microsoft.com/library/windows/hardware/mt297559)。

 

 





