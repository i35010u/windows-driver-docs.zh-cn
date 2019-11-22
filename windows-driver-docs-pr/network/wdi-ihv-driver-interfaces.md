---
title: WDI IHV 驱动程序接口
description: WDI IHV 小型端口与任何其他 NDIS 微型端口驱动程序类似，它将遵循适用于任何 NDIS 小型端口的开发实践和文档。
ms.assetid: B4528C70-9FE4-4E00-9D0B-8832CCEC982E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec567a375806ae73477c015caf86c078f38db260
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842926"
---
# <a name="wdi-ihv-driver-interfaces"></a>WDI IHV 驱动程序接口


WDI IHV 小型端口与任何其他 NDIS 微型端口驱动程序类似，它将遵循适用于任何 NDIS 小型端口的开发实践和文档。 本机 WLAN 微型端口驱动程序在 MS 组件和 WDI IHV 驱动程序之间拆分了 NDIS 处理程序的责任。 Microsoft WLAN 组件负责处理适用于所有 Wi-fi 微型端口的 NDIS 要求，使每个 IHV 不必重做所有工作。 下面描述了在应用于 WDI IHV 微型端口的情况下，对本机 WLAN IHV 小型端口的 NDIS 处理程序的和行为更改。

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
-   [WDI 处理程序： MiniportWdiOpenAdapter](#wdi-handler-miniportwdiopenadapter)
-   [WDI 处理程序： MiniportWdiCloseAdapter](#wdi-handler-miniportwdicloseadapter)

## <a name="driver-installation"></a>驱动程序安装


WDI IHV 微型端口驱动程序在系统上的加载和安装方式没有变化。 INF 和安装过程类似于 IHV 本机 WLAN 微型端口驱动程序。 与现有 NDIS 驱动程序一样，当需要加载 IHV 驱动程序以与 IHV 的 WLAN 适配器一起工作时，操作系统将调用 IHV 微型端口驱动程序的 DriverEntry 例程。

## <a name="driverentry"></a>DriverEntry


操作系统直接调用 WDI IHV 微型端口驱动程序的 DriverEntry 例程。 IHV 微型端口遵循常规 NDIS 微型端口的 DriverEntry 例程的大部分准则。 但有一个例外，就是不调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)，而是使用 IHV 微型端口调用[**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)来告知操作系统启用 Microsoft WLAN 组件。

下面是[**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)的关键参数。

-   [**NDIS\_微型端口\_驱动程序\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)：这是本机 wi-fi 小型端口用于注册 NDIS 的原始 NDIS 结构。 对于 WDI 模型，大部分处理程序参数都是可选的。 唯一必需的处理程序是 **\_OID\_请求\_处理程序**和**微型端口\_驱动程序\_卸载**的小型端口。 **\_OID\_请求\_处理程序使用的微型端口**将 WDI 消息传递到 IHV 驱动程序。 如果指定了其他任何处理程序，则 Microsoft WLAN 组件通常会在对处理程序执行自己的处理后调用该处理程序。
-   [**NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)：这是 WDI 微型端口驱动程序必须实现的一组新的处理程序。 IHV 驱动程序使用它为控制路径注册其他处理程序，并使用数据路径的完整处理程序集。

当 IHV 小型端口调用 NdisMRegisterWdiMiniportDriver 时，Microsoft WLAN 组件会更新[**NDIS\_微型\_驱动程序\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)的处理程序，并调用 Ndis 的[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)。 更新完成后，Microsoft WLAN 组件便可截获可为其提供帮助/简化的处理程序，以 WDI IHV 微型端口驱动程序。

下面是 WDI IHV 微型端口驱动程序的典型流程 DriverEntry 流程

![wdi driverentry 流](images/wdi-driverentry-flow.png)

有关 DriverEntry 的详细信息，请参阅[**DriverEntry OF NDIS 微型端口驱动程序**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)。

## <a name="miniportsetoptions"></a>MiniportSetOptions


如上面的 DriverEntry 关系图所示，如果 WDI IHV 微型端口已注册[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)处理程序，则操作系统会在调用[**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)的微型端口驱动程序的上下文中调用该函数。

如果 IHV 微型端口驱动程序使用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)注册任何选项处理程序，则这些处理程序可能不会通过 Microsoft 组件通过 WDI 层进行序列化。 因此，IHV 组件负责处理这些处理程序的任何同步要求。

## <a name="miniportinitializeex"></a>MiniportInitializeEx


WDI 模型将[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)行为拆分为多个 WDI 接口调用。

1.  调用[*MiniportWdiAllocateAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_allocate_adapter)。

    当操作系统查找 IHV 硬件的实例时，这是第一次调用 WDI IHV 微型端口驱动程序。 在此调用中，WDI 微型端口执行创建设备的软件表示（**MiniportAdapterContext**）所需的操作。 它还确定了有关设备的信息以在[**NDIS\_微型端口\_适配器\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构中填充。 以后，当 Microsoft 组件发送 WDI 命令来执行特定的初始化时，设备和 Wi-fi 堆栈的实际初始化将会完成。

    使用从 WDI IHV 微型端口驱动程序获得的数据，Microsoft 组件会调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并设置[**NDIS\_微型端口\_适配器\_注册\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)。 默认情况下，Microsoft 组件使用默认值填充**NDIS\_微型端口\_适配器\_注册\_属性**的大多数字段。 IHV 驱动程序必须填充**MiniportAdapterContext**和**InterfaceType**字段。

    此调用从 IHV 微型端口驱动程序返回后，将开始通过其[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)处理程序接收 WDI 命令。 在此调用过程中，Microsoft 组件可能无法执行重置/恢复操作，因此在此处执行的任何活动都应该快速可靠。

2.  调用[*MiniportWdiOpenAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)。

    [*MiniportWdiAllocateAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_allocate_adapter)后，Microsoft 组件会调用[*MiniportWdiOpenAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)来加载固件并初始化硬件。

3.  使用[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)的多个 WDI 命令。

    [*MiniportWdiOpenAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)后，Microsoft 组件会将以下任务/属性/调用发送到 IHV 小型端口。

    1.  调用[*MiniportWdiTalTxRxInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_initialize)以初始化数据路径和 exchange 处理程序。
    2.  调用[OID\_WDI\_获取\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)，以获取适配器的功能。
    3.  调用[OID\_WDI\_设置\_适配器\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-adapter-configuration)以配置适配器。
    4.  调用[OID\_WDI\_任务\_设置\_无线电\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-set-radio-state)，以设置初始无线电状态（如果尚未处于预期状态）。
    5.  调用[*MiniportWdiTalTxRxStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_start)设置数据路径。
    6.  调用[OID\_WDI\_任务\_创建\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)以创建初始端口。

    其他命令还可以被发送到 IHV 组件，作为 Microsoft 组件的 MiniportInitializeEx 处理的一部分。 但是，在调用[*MiniportWdiStartOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_start_adapter_operation)之前，Microsoft 组件不会发送任何需要无线通信的任务。 除了[OID\_WDI\_任务\_OPEN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-open)总是首先发送，其他命令/调用的顺序可能会更改。

    使用从 WDI IHV 微型端口驱动程序获得的数据，Microsoft 组件会调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)并设置[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)和[**NDIS\_微型端口\_适配器\_本机\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85))。

4.  调用[*MiniportWdiStartOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_start_adapter_operation)。

    这是[**NDIS\_微型端口\_驱动程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)中的可选 WDI 微型端口处理程序\_WDI\_特性，IHV 驱动程序可以使用这些特性执行任何其他 MiniportInitializeEx 任务。 它还可由 IHV 小型端口使用，作为提示，Microsoft 组件已完成初始化微型端口，并且微型端口可以启动任何所需的后台活动。

    下图显示了 MiniportInitializeEx 的 flow。

    ![wdi 微型端口初始化流](images/wdi-miniport-initialization-flow.png)

    如果中间操作失败，Microsoft 组件会撤消之前的操作，并使微型端口出现故障。 例如，如果[OID\_WDI\_任务\_创建\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)失败，则会清除数据路径、 [OID\_WDI\_任务\_关闭](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-close)，并且微型端口会失败。

## <a name="miniporthaltex"></a>MiniportHaltEx


在本机 Wi-fi 小型端口中， [*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)用于指示微型端口停止操作并清理适配器实例。 在 WDI 模型中，Microsoft 组件处理原始*MiniportHaltEx*调用并将其拆分为多个 WDI 接口调用。

1.  调用[*MiniportWdiStopOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_stop_adapter_operation)。

    这是[**NDIS\_微型端口\_驱动程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)中的可选 WDI 微型端口处理程序\_WDI\_特性，IHV 驱动程序可以使用这些特性来撤消它在[*MiniportWdiStartOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_start_adapter_operation)中所执行的操作。

2.  使用[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)的多个 WDI 命令。

    [*MiniportWdiStopOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_stop_adapter_operation)后，Microsoft 组件会将任务/属性发送到 ihv 小型端口，以清理 ihv 驱动程序的当前状态。 此清理可能包括以下。

    1.  调用[OID\_WDI\_任务\_断开](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-disconnect)/[OID\_WDI\_TASK\_停止\_AP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-stop-ap)以切断任何现有连接。
    2.  [\_WDI\_任务调用 OID，\_删除\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-delete-port)以删除所有已创建的端口。
    3.  调用[*MiniportWdiTalTxRxStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_stop)停止数据路径。
    4.  调用[*MiniportWdiTalTxRxDeinitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_deinitialize) deinitialize 数据路径。
    5.  调用以清理硬件状态。 使用已由 IHV 驱动程序注册的[*MiniportWdiCloseAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_close_adapter)将其发送到 ihv。

3.  调用上述所有命令后，Microsoft 组件会调用[*MiniportWdiFreeAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_free_adapter) ，以使 IHV 驱动程序删除其可能具有的任何软件状态。

下图显示了 MiniportHaltEx 的 flow。

![wdi 微型端口暂停流](images/wdi-miniport-halt-flow.png)

如果设备被意外删除或系统正在关闭，则不会执行 MiniportHaltEx 处理。 有关意外删除，请参阅[MiniportDevicePnPEventNotify](#miniportdevicepnpeventnotify)处理程序行为。 对于系统关闭，请参阅[MiniportShutdownEx](#miniportshutdownex)处理程序行为。

## <a name="miniportdriverunload"></a>MiniportDriverUnload


[*MiniportDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)是卸载 WDI IHV 微型端口之前调用的处理程序。 WDI IHV 微型端口驱动程序调用 Microsoft 组件以便自行取消注册。 Microsoft 组件调用[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)。

下图显示了 MiniportDriverUnload 的 flow。

![wdi 微型端口驱动程序卸载流](images/wdi-miniport-driver-unload-flow.png)

## <a name="miniportpause"></a>MiniportPause


NDIS [*MiniportPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)要求由 Microsoft 组件处理。 作为 MiniportPause 的一部分，Microsoft 组件会停止数据路径，并等待它进行清理。 WDI IHV 微型端口可以选择注册[*MiniportWdiPostAdapterPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_post_adapter_pause)回调，在完成数据路径清理后，由 Microsoft 组件调用。

下图显示了 MiniportPause 的 flow。

![wdi 微型端口暂停流](images/wdi-miniport-pause-flow.png)

## <a name="miniportrestart"></a>MiniportRestart


NDIS [*MiniportRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)要求由 Microsoft 组件处理。 作为 MiniportRestart 的一部分，Microsoft 组件会撤消它作为 MiniportPause 的一部分执行的数据路径暂停工作。 WDI IHV 微型端口可以选择注册[*MiniportWdiPostAdapterRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_post_adapter_restart)回调，该回调由 Microsoft 组件在完成重新启动数据路径后调用。

下图显示了 MiniportRestart 的 flow。

![wdi 微型端口重启流](images/wdi-miniport-restart-flow.png)

## <a name="miniportresetex"></a>MiniportResetEx


[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)不由 Microsoft 组件处理。 WDI IHV 微型端口可以选择注册 Microsoft 组件调用的*MiniportResetEx*回调。

## <a name="miniportdevicepnpeventnotify"></a>MiniportDevicePnPEventNotify


[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)用于向 NDIS 驱动程序通知 PNP 事件，例如设备的意外删除。 当 NDIS 发送此通知时，它将首先转发到 WDI IHV 微型端口进行处理。 在 IHV 组件完成对它的处理后，Microsoft 组件将为此事件执行适当的处理。 转发到 IHV 组件的调用不会与其他任务和回调序列化。

下图显示了 MiniportDevicePnPEventNotify 的 flow。

![wdi 微型端口驱动器 pnp 通知流](images/wdi-miniport-device-pnp-notification-flow.png)

## <a name="miniportshutdownex"></a>MiniportShutdownEx


[*MiniportShutdownEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)用于通知 NDIS 驱动程序关于系统关闭事件。 当 NDIS 发送此通知时，它将由 Microsoft 组件首先处理。 Microsoft 组件完成处理后，会将事件传递给 WDI IHV 小型端口进行处理。

下图显示了 MiniportShutdownEx 的 flow。

![wdi 微型端口关闭流](images/wdi-miniport-shutdown-flow.png)

## <a name="miniportoidrequest"></a>MiniportOidRequest


[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)处理程序是 WDI IHV 微型端口必须实现的必需处理程序。 它由 Microsoft 组件用来向 IHV 小型端口提交 WDI 命令。 它还用于转发 Microsoft 组件未处理到 IHV 小型端口的 Oid。

将[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)调用到 WDI IHV 微型端口应视为 WDI 命令的 M1 消息。 完成 OID （通过[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)或通过*MiniportOidRequest*的返回非挂起）的完成应视为 WDI 任务/命令的 M3 消息。

对于每个 WDI 命令，都有两个可能的字段可用于为操作返回 NDIS\_状态代码- [*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)调用中的状态代码（或[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)），以及 WDI 中的状态代码[ **\_消息\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)字段（在 OID 完成或 Via [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)上）。 Microsoft 组件始终从 OID 完成中查看 NDIS\_状态，然后再查看**WDI\_MESSAGE\_HEADERStatus**字段。 WDI OID 处理的 IHV 组件的预期如下所示。

1.  WDI Oid 使用[ **\_请求 RequestType 的 NDIS\_OID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)提交到 IHV 组件，并且相应的消息和消息长度位于**数据中。方法\_InformationBuffer**和**数据。方法\_信息。InputBufferLength**字段。
2.  如果处理该命令时出现错误，则 IHV 组件会报告 OID 完成中的错误，并将[**WDI\_MESSAGE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)的状态字段设置为 "不成功" （如果它具有 wi-fi 级别故障）。
3.  对于任务和属性，请求的端口号位于[**WDI\_MESSAGE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)**PortId**字段中。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)中的**PortNumber**始终设置为0。
4.  完成 OID 后， [*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)可通过[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)将 NDIS\_\_状态返回到 "挂起"，并在以后（以同步或异步方式）完成 oid。
5.  如果 IHV 组件完成 OID\_状态为\_SUCCESS，则必须用适当的字节数（包括[**WDI\_消息\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)的空间）填充 oid 请求的**BytesWritten**字段.
6.  如果 IHV 组件在数据中没有足够的空间 **。方法\_信息。OutputBufferLength**字段填充响应后，它将完成具有 NDIS\_状态\_缓冲区的 OID\_\_太短并填充**数据。方法\_信息。BytesNeeded**字段。 Microsoft 组件可能会尝试分配一个请求大小的缓冲区，并向 IHV 提交新的请求。
7.  如果该任务是任务，则只有在任务被报告为已成功启动时才必须指示任务的 M4 （[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)）--oid 完成成功，且 WDI 中的**状态** [ **\_消息中\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)已成功完成。

下图显示了映射到单个 WDI 命令的 NDIS OID 请求的示例。 当由操作系统提交 OID 请求时，Microsoft 组件会将其转换为 WDI OID 请求，并将 WDI OID 请求提交到 IHV 小型端口。 当 IHV 微型端口完成 OID 时，Microsoft 组件会适当地完成原始 OID 请求。

![单个 wdi 命令的 wdi 微型端口 oid 请求序列](images/wdi-miniport-oid-request-single.png)

如果 OriginalOidRequest 映射到多个 WDI OidRequests，其中一个 WDI 请求失败，则 OriginalOidRequest 也会失败。 如果已完成了中间操作的一个子集，则 Microsoft 组件会尝试撤消支持清理操作的操作。

下图显示了由 Microsoft 组件完成的 NDIS OID 请求的示例。 当由操作系统提交 OID 请求时，Microsoft 组件会处理并完成 OID。 此 OID 不会传递到 WDI IHV 微型端口。

![microsoft 组件处理的 oid 的 wdi 微型端口 oid 请求序列](images/wdi-miniport-oid-request-wdi-handled.png)

Microsoft 组件不能理解的 Oid 会直接转发到 IHV 组件进行处理。

![microsoft 组件未处理的 oid 的 wdi 微型端口 oid 请求序列](images/wdi-miniport-oid-request-unknown.png)

对于 WDI IHV 微型端口驱动程序（与本机 Wi-fi 小型端口相比），MiniportOidRequest 的行为不变。 调用将进行序列化，并且 IHV 微型端口可以通过调用[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)以同步或异步方式完成调用。

## <a name="miniportcanceloidrequest"></a>MiniportCancelOidRequest


这是一个可选的处理程序，由需要处理未映射到 WDI 消息的 Oid 的 WDI IHV 微型端口使用。 此处理程序不用于任何 WDI Oid。 WDI Oid 必须迅速完成，并且不需要使用 IHV 微型端口驱动程序来尝试取消挂起的 OID。 使用适当的取消任务 OID 请求来处理 WDI 任务的取消。 对于未映射的 Oid，预期的行为由 NDIS 定义。

## <a name="ndismindicatestatusex"></a>NdisMIndicateStatusEx


WDI IHV 微型端口使用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)将指示发送到 Microsoft 组件。 指示可能是不受请求的指示，如 TKIP MIC 故障，也可能是任务完成（M4）的请求指示。

下图显示了一个 WDI 指示的示例，该示例具有相应的 NDIS/Native Wi-fi 指示。 当由 IHV 微型端口向 Microsoft 组件提交指示时，Microsoft 组件会将其转换为现有指示，并将其转发到操作系统。

![wdi 微型端口状态指示流](images/wdi-miniport-status-indication-flow.png)

下图显示了一个 WDI 指示的示例，该指示没有相应的 NDIS/本机 Wi-fi 指示。 这由 Microsoft 组件处理。

![wdi 状态指示，不直接映射到 ndis](images/wdi-miniport-status-indication-not-ndis.png)

下图显示了 Microsoft 组件无法识别的指示。 指示会按原样转发到操作系统。

![wdi 状态指示无法被 microsoft 组件识别](images/wdi-miniport-status-indication-unknown.png)

对于 WDI IHV 微型端口驱动程序（与本机 Wi-fi 小型端口相比），NdisMIndicateStatusEx 的行为不变。

## <a name="miniportdirectoidrequest"></a>MiniportDirectOidRequest


如果 WDI IHV 微型端口驱动程序需要处理未映射到 WDI 消息的直接 Oid，则这是一个可选的处理程序。 Wi-fi Direct 的所有现有直接 Oid 都映射到 WDI 消息，因此不需要此处理程序来支持该功能。 不支持的直接 Oid 不由 Microsoft 组件序列化。

## <a name="miniportcanceldirectoidrequest"></a>MiniportCancelDirectOidRequest


这是一个可选的处理程序，由需要处理未映射到 WDI 消息的直接 Oid 的 WDI IHV 小型端口使用。 对于未映射的 Oid，预期的行为由 NDIS 定义。

## <a name="miniportsendnetbufferlists"></a>MiniportSendNetBufferLists


此处理程序不在 WDI IHV 微型端口驱动程序中使用，因此不应提供。 Microsoft 组件使用通过 NDIS 注册的数据路径处理程序[ **\_微型端口\_驱动程序\_WDI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)，将发送数据包提交到 IHV 小型端口。

## <a name="miniportcancelsend"></a>MiniportCancelSend


此处理程序不在 WDI IHV 微型端口驱动程序中使用，因此不应提供。

## <a name="miniportreturnnetbufferlists"></a>MiniportReturnNetBufferLists


此处理程序不在 WDI IHV 微型端口驱动程序中使用，因此不应提供。 Microsoft 组件使用通过 NDIS 注册的数据路径处理程序[ **\_微型端口\_驱动程序\_WDI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)将接收的数据包返回到 IHV 小型端口。

## <a name="wdi-handler-miniportwdiopenadapter"></a>WDI 处理程序： MiniportWdiOpenAdapter


Microsoft 组件使用[*MiniportWdiOpenAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)处理程序在 IHV 驱动程序上启动 "打开任务" 操作。 此调用必须迅速完成，如果打开操作已成功启动，则 IHV 必须返回 NDIS\_状态，\_成功进行此调用，并调用传递到 NDIS\_WDI 的[**OpenAdapterComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_open_adapter_complete)处理程序[ **\_INIT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters) [*MINIPORTWDIALLOCATEADAPTER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_allocate_adapter)的参数参数。

## <a name="wdi-handler-miniportwdicloseadapter"></a>WDI 处理程序： MiniportWdiCloseAdapter


Microsoft 组件使用[*MiniportWdiCloseAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_close_adapter)处理程序来启动对 IHV 驱动程序的关闭任务操作。 此调用必须迅速完成，如果打开操作已成功启动，则 IHV 必须返回 NDIS\_状态\_"成功" 此调用，并调用传递到\_Ndis 的[**CloseAdapterComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_close_adapter_complete)处理程序，该处理程序会传递到[*MiniportWdiAllocateAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_allocate_adapter)的[**WDI\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)参数中。

 

 





