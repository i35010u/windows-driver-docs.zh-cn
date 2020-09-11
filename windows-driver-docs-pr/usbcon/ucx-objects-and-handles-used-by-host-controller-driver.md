---
description: UCX 扩展了 WDF 对象功能，以定义其自己的特定于 USB 的 UCX 对象。 UCX 使用这些对象将请求排队到任何基础主机控制器驱动程序。
title: 主控制器驱动程序使用的 UCX 对象和句柄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3c4db1e30236e307ed4aafe7e4d7b30701119ec
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009804"
---
# <a name="ucx-objects-and-handles-used-by-a-host-controller-driver"></a>主控制器驱动程序使用的 UCX 对象和句柄


**摘要**

-   主机控制器驱动程序使用 UCX 对象来处理与控制器、其根集线器和所有终结点相关的操作。
-   UCX 对象由主机控制器驱动程序创建，每个对象的生存期由 UCX 管理。

**适用于**

-   Windows 10

**上次更新时间**

-   2015 年 7 月

**重要的 API**

-   [**UcxControllerCreate**](/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))
-   [**UcxRootHubCreate**](/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))
-   [**UcxUsbDeviceCreate**](/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)

UCX 扩展了 WDF 对象功能，以定义其自己的特定于 USB 的 UCX 对象。 UCX 使用这些对象将请求排队到任何基础主机控制器驱动程序。

有关 WDF 对象的更多详细信息，请参阅 [框架对象简介](../wdf/introduction-to-framework-objects.md)。

## <a name="host-controller-object"></a>主机控制器对象


**UCXCONTROLLER**

表示主机控制器驱动程序创建的主控制器。 驱动程序必须为每个主机控制器实例仅创建一个主机控制器对象。 通常通过调用[**UcxControllerCreate**](/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))方法在[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调中创建。

当主机控制器驱动程序创建对象时，驱动程序将注册由 UCX 调用的回调函数的实现。 驱动程序还应另外标识用于连接主机控制器的总线类型，如 ACPI 或 PCI。 该驱动程序还通过使用传递给[**UcxControllerCreate**](/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))调用的[**UCX \_ 控制器 \_ 配置**](/windows-hardware/drivers/ddi/ucxcontroller/ns-ucxcontroller-_ucx_controller_config)结构来提供主机控制器设备信息。

若要处理 i/o 请求，主机控制器驱动程序必须注册 GUID \_ DEVINTERFACE \_ USB \_ 主机 \_ 控制器设备接口。 该驱动程序不是实现此接口中定义的 IOCTLs 所必需的。 相反，UCX 客户端通过调用 [**UcxIoDeviceControl**](/windows-hardware/drivers/ddi/ucxcontroller/nf-ucxcontroller-ucxiodevicecontrol)将此接口上收到的 IOCTL 请求传递到 UCX。

下面是与宿主控制器对象关联的回调函数，由 UCX 调用。 这些函数必须由主机控制器驱动程序实现。

[*.EVT \_ UCX \_ 控制器 \_ USBDEVICE \_ 添加*](/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add)  
当集线器驱动程序已确定时，通过与根集线器和/或外部集线器 (s) 交互，在总线上出现新的设备。

[*.EVT \_ UCX \_ 控制器 \_ 查询 \_ USB \_ 功能*](/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_query_usb_capability)  
由 UCX 调用，用于收集有关 USB 主机控制器支持的各种功能的信息。

[*.EVT \_ UCX \_ 控制器 \_ 重置*](/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_reset)  
由 UCX 调用以重置控制器硬件，可能是为了响应检测到的错误。

[*.EVT \_ UCX \_ 控制器 \_ 获取 \_ 当前 \_ FRAMENUMBER*](/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_get_current_framenumber)  
用于从主机控制器检索当前帧号，集线器驱动程序使用该数字来计划同步传输。

## <a name="root-hub-object"></a>根中心对象


**UCXROOTHUB**

获取和控制主机控制器的根端口的状态。 在创建主机控制器对象之后，通过调用[**UcxRootHubCreate**](/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))方法，在[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调中通常由主机控制器驱动程序创建。 每个主机控制器实例只能有一个根中心对象。 在 **UcxRootHubCreate** 调用中，驱动程序将注册其回调实现。

[*.EVT \_ UCX \_ ROOTHUB \_ 获取 \_ 信息*](/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_info)  
返回根集线器的 USB 2.0 和 USB 3.0 端口的数量。

[*.EVT \_ UCX \_ ROOTHUB \_ 获取 \_ 20PORT \_ 信息*](/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_20port_info)  
返回有关 USB 2.0 或 USB 3.0 端口的信息 ([*.Evt \_ UCX \_ ROOTHUB 获取根集线器的 \_ \_ 30PORT \_ 信息*](/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_30port_info)) 。

创建并初始化根中心对象后，集线器驱动程序通过发送中断和控制传输与根集线器端口交互。 UCX 通过调用主机控制器驱动程序实现的这些回调函数来帮助进行这些传输。

[*.EVT \_ UCX \_ ROOTHUB \_ 控制 \_ URB*](/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_control_urb)  
处理 USB 集线器的功能控制请求。

[*.EVT \_ UCX \_ ROOTHUB \_ 中断 \_ TX*](/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_interrupt_tx)  
处理有关已更改端口的信息请求。

有关详细信息，请参阅 [主机控制器驱动程序的根集线器回叫函数](manage-the-root-hub-in-a-host-controller-driver.md)。

## <a name="usb-device-object"></a>USB 设备对象


**UCXUSBDEVICE**

表示连接到总线的物理 USB 设备。 由主机控制器驱动程序创建，通常在 [*.Evt \_ UCX \_ controller \_ USBDEVICE \_ *](/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add) 中，通过调用 [**UcxUsbDeviceCreate**](/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate) 方法添加回调。

当创建对象时，主机控制器驱动程序会通过 [**UcxUsbDeviceCreate**](/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate) 调用来注册其回调函数的实现。

这些回调函数旨在使控制器和驱动程序知道 USB 设备的当前状态。

[*.EVT \_ UCX \_ USBDEVICE \_ ENABLE*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_enable)  
准备控制器以执行到设备的默认终结点的传输。

[*.EVT \_ UCX \_ USBDEVICE \_ DISABLE*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)  
释放与设备及其默认终结点关联的控制器资源。

[*.EVT \_ UCX \_ USBDEVICE \_ 地址*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_address)  
将地址写入控制器并向设备发送一组 \_ 地址传输，以使其进入 "已解决" 状态。

[*.EVT \_ UCX \_ USBDEVICE \_ 终结点 \_ 配置*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoints_configure)  
在控制器中计划非默认终结点，并/或释放其他非默认终结点。

[*.EVT \_ UCX \_ USBDEVICE \_ RESET*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_reset)  
已重置设备的控制器通知，在这种情况下，驱动程序将采取任何必要的操作将控制器与 USB 设备同步。

[*.EVT \_ UCX \_ USBDEVICE \_ 更新*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_update)  
通知控制器与设备相关的各种信息。

[*.EVT \_ UCX \_ USBDEVICE \_ HUB \_ 信息*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_hub_info)  
有关集线器属性的通知（如果 UCXUSBDEVICE 句柄适用于集线器设备）。

[*.EVT \_ UCX \_ USBDEVICE \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)  
通知驱动程序为设备创建终结点。 [*.Evt \_UCX \_ USBDEVICE \_ \_ \_ *](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add) 默认终结点添加默认终结点。

当挂起的 USB 3.0 设备上的接口唤醒时，驱动程序应调用 [**UcxUsbDeviceRemoteWakeNotification**](/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdeviceremotewakenotification) 来通知 UCX。

创建对象后，对象的生存期由 UCX 管理，驱动程序不能删除该对象。

## <a name="endpoint-object"></a>终结点对象


**UCXENDPOINT**

表示 USB 设备对象上的终结点。 在 [* \_ UCX \_ USBDEVICE \_ 默认 \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add) 或 [*.evt \_ UCX \_ USBDEVICE \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add) 回调期间，主机控制器会创建终结点对象。 创建终结点对象时，驱动程序将注册其回调函数。

驱动程序还会为每个终结点创建一个框架队列对象，并通过调用 [**UcxEndpointSetWdfIoQueue**](/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointsetwdfioqueue)将该队列的 WDFQUEUE 传递到 UCX。 创建终结点后，该对象及其关联队列的生存期由 UCX 管理，驱动程序不能删除这些对象本身。

终结点对象实现了多个回调函数，使驱动程序能够帮助 UCX 与终结点相关的操作。

[*.EVT \_ UCX \_ 终结点 \_ 中止*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_abort)  
中止与终结点关联的队列。

[*.EVT \_ UCX \_ 终结 \_ 点 \_ 可 \_ 取消 \_ 传输*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)  
通知控制器驱动程序它可以在终结点上完成已取消的传输。

[*.EVT \_ UCX \_ 终结点 \_ 清除*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_purge)  
在终结点上完成所有未完成的 i/o 请求。

[*.EVT \_ UCX \_ 终结点 \_ 启动*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_start)  
启动与终结点关联的队列。

[*.EVT \_ UCX \_ 终结点 \_ 静态 \_ 流 \_ 添加*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)  
创建静态流。

[*.EVT \_ UCX \_ 终结点 \_ 重置*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_reset)  
通知驱动程序重置控制器的终结点编程。

当主机控制器驱动程序在终结点上收到 USB 3.0 无 Ping 响应错误时，驱动程序必须调用 [**UcxEndpointNoPingResponseError**](/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointnopingresponseerror)。 该调用将导致接收 [*.Evt \_ UCX \_ USBDEVICE \_ 更新*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_update)的 USB 设备对象。
有关详细信息，请参阅 [在主机控制器驱动程序中配置 USB 端点](configuring-usb-endpoints-in-a-host-controller-driver.md)。

## <a name="stream-object"></a>Stream 对象


**UCXSTREAMS**

表示单个终结点到设备的多个管道。 主机控制器驱动程序通过调用[**UcxStaticStreamsCreate**](/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)在[*.Evt UCX 终结点中创建流对象 \_ \_ \_ 静态 \_ 流 \_ 添加*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)回调。

在 [**UcxStaticStreamsCreate**](/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate) 调用期间，主机控制器驱动程序将注册其回调函数。 对于特定的终结点对象，驱动程序可以确定它是否已创建流对象，并通过调用 [**UcxEndpointGetStaticStreamsReferenced**](/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointgetstaticstreamsreferenced)返回 UCXSTREAMS 句柄。

创建对象后，驱动程序将为每个流创建一个框架队列对象，并通过调用 [**UcxStaticStreamsSetStreamInfo**](/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamssetstreaminfo)将 WDFQUEUE 句柄发送到 UCX。

Stream 对象为主机控制器提供了若干回调函数，以帮助 UCX 管理静态流。

[*.EVT \_ UCX \_ 终结点 \_ 静态 \_ 流 \_ 禁用*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_disable)  
为终结点的所有流释放控制器资源。

[*.EVT \_ UCX \_ 终结点 \_ 静态 \_ 流 \_ 启用*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_enable)  
为此终结点启用所有流的控制器硬件。

对象的生存期和关联的队列由 UCX 管理，驱动程序不能删除这些对象。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)