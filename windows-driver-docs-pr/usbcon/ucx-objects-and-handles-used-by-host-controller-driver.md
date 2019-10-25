---
Description: UCX 扩展了 WDF 对象功能，以定义其自己的特定于 USB 的 UCX 对象。 UCX 使用这些对象将请求排队到任何基础主机控制器驱动程序。
title: 主控制器驱动程序使用的 UCX 对象和句柄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cea15160b2da02d540a0689aabe7b7c3882eb65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844340"
---
# <a name="ucx-objects-and-handles-used-by-a-host-controller-driver"></a>主控制器驱动程序使用的 UCX 对象和句柄


**摘要**

-   主机控制器驱动程序使用 UCX 对象来处理与控制器、其根集线器和所有终结点相关的操作。
-   UCX 对象由主机控制器驱动程序创建，每个对象的生存期由 UCX 管理。

**适用于**

-   Windows 10

**上次更新时间**

-   2015 年 7 月

**重要的 API**

-   [**UcxControllerCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))
-   [**UcxRootHubCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))
-   [**UcxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)

UCX 扩展了 WDF 对象功能，以定义其自己的特定于 USB 的 UCX 对象。 UCX 使用这些对象将请求排队到任何基础主机控制器驱动程序。

有关 WDF 对象的更多详细信息，请参阅[框架对象简介](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)。

## <a name="host-controller-object"></a>主机控制器对象


**UCXCONTROLLER**

表示主机控制器驱动程序创建的主控制器。 驱动程序必须为每个主机控制器实例仅创建一个主机控制器对象。 通常通过调用[**UcxControllerCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))方法在[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调中创建。

当主机控制器驱动程序创建对象时，驱动程序将注册由 UCX 调用的回调函数的实现。 驱动程序还应另外标识用于连接主机控制器的总线类型，如 ACPI 或 PCI。 该驱动程序还通过使用传递给[**UcxControllerCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))调用的[**UCX\_控制器\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/ns-ucxcontroller-_ucx_controller_config)结构来提供主机控制器设备信息。

若要处理 i/o 请求，主机控制器驱动程序必须将 GUID\_DEVINTERFACE\_USB\_主机\_控制器设备接口。 该驱动程序不是实现此接口中定义的 IOCTLs 所必需的。 相反，UCX 客户端通过调用[**UcxIoDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nf-ucxcontroller-ucxiodevicecontrol)将此接口上收到的 IOCTL 请求传递到 UCX。

下面是与宿主控制器对象关联的回调函数，由 UCX 调用。 这些函数必须由主机控制器驱动程序实现。

[ *.EVT\_UCX\_控制器\_USBDEVICE\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add)  
当集线器驱动程序通过与根集线器和/或外部集线器交互，在总线上存在新设备时，会调用。

[ *.EVT\_UCX\_控制器\_查询\_USB\_功能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_query_usb_capability)  
由 UCX 调用，用于收集有关 USB 主机控制器支持的各种功能的信息。

[ *.EVT\_UCX\_控制器\_重置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_reset)  
由 UCX 调用以重置控制器硬件，可能是为了响应检测到的错误。

[ *.EVT\_UCX\_控制器\_获取\_当前\_FRAMENUMBER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_get_current_framenumber)  
用于从主机控制器检索当前帧号，集线器驱动程序使用该数字来计划同步传输。

## <a name="root-hub-object"></a>根中心对象


**UCXROOTHUB**

获取和控制主机控制器的根端口的状态。 在创建主机控制器对象之后，通过调用[**UcxRootHubCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))方法，在[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调中通常由主机控制器驱动程序创建。 每个主机控制器实例只能有一个根中心对象。 在**UcxRootHubCreate**调用中，驱动程序将注册其回调实现。

[ *.EVT\_UCX\_ROOTHUB\_获取\_信息*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_info)  
返回根集线器的 USB 2.0 和 USB 3.0 端口的数量。

[ *.EVT\_UCX\_ROOTHUB\_获取\_20PORT\_信息*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_20port_info)  
返回有关根集线器的 USB 2.0 或 USB 3.0 端口（[ *.evt\_UCX\_ROOTHUB\_获取\_30PORT\_信息*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_30port_info)）的信息。

创建并初始化根中心对象后，集线器驱动程序通过发送中断和控制传输与根集线器端口交互。 UCX 通过调用主机控制器驱动程序实现的这些回调函数来帮助进行这些传输。

[ *.EVT\_UCX\_ROOTHUB\_控件\_URB*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_control_urb)  
处理 USB 集线器的功能控制请求。

[ *.EVT\_UCX\_ROOTHUB\_中断\_TX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_interrupt_tx)  
处理有关已更改端口的信息请求。

有关详细信息，请参阅[主机控制器驱动程序的根集线器回叫函数](manage-the-root-hub-in-a-host-controller-driver.md)。

## <a name="usb-device-object"></a>USB 设备对象


**UCXUSBDEVICE**

表示连接到总线的物理 USB 设备。 通常由主机控制器驱动程序创建[ *\_UCX\_控制器\_USBDEVICE\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add)通过调用[**UcxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)方法添加回调。

当创建对象时，主机控制器驱动程序会通过[**UcxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)调用来注册其回调函数的实现。

这些回调函数旨在使控制器和驱动程序知道 USB 设备的当前状态。

[ *.EVT\_UCX\_USBDEVICE\_启用*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_enable)  
准备控制器以执行到设备的默认终结点的传输。

[ *.EVT\_UCX\_USBDEVICE\_禁用*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)  
释放与设备及其默认终结点关联的控制器资源。

[ *.EVT\_UCX\_USBDEVICE\_地址*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_address)  
将一个地址写入控制器并将一组\_地址传输发送到设备，以使其进入 "已解决" 状态。

[ *.EVT\_UCX\_USBDEVICE\_终结点\_配置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoints_configure)  
在控制器中计划非默认终结点，并/或释放其他非默认终结点。

[ *.EVT\_UCX\_USBDEVICE\_重置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_reset)  
已重置设备的控制器通知，在这种情况下，驱动程序将采取任何必要的操作将控制器与 USB 设备同步。

[ *.EVT\_UCX\_USBDEVICE\_更新*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_update)  
通知控制器与设备相关的各种信息。

[ *.EVT\_UCX\_USBDEVICE\_集线器\_信息*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_hub_info)  
有关集线器属性的通知（如果 UCXUSBDEVICE 句柄适用于集线器设备）。

[ *.EVT\_UCX\_USBDEVICE\_\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)  
通知驱动程序为设备创建终结点。 [ *.Evt\_UCX\_USBDEVICE\_默认\_终结点\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add)默认终结点。

当挂起的 USB 3.0 设备上的接口唤醒时，驱动程序应调用[**UcxUsbDeviceRemoteWakeNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdeviceremotewakenotification)来通知 UCX。

创建对象后，对象的生存期由 UCX 管理，驱动程序不能删除该对象。

## <a name="endpoint-object"></a>终结点对象


**UCXENDPOINT**

表示 USB 设备对象上的终结点。 终结点对象由主机控制器在[ *\_UCX\_USBDEVICE\_默认\_终结点中创建，\_添加或默认终结*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add)点\_\_[*添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)拨. 创建终结点对象时，驱动程序将注册其回调函数。

驱动程序还会为每个终结点创建一个框架队列对象，并通过调用[**UcxEndpointSetWdfIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointsetwdfioqueue)将该队列的 WDFQUEUE 传递到 UCX。 创建终结点后，该对象及其关联队列的生存期由 UCX 管理，驱动程序不能删除这些对象本身。

终结点对象实现了多个回调函数，使驱动程序能够帮助 UCX 与终结点相关的操作。

[ *\_UCX\_终结点\_中止*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_abort)  
中止与终结点关联的队列。

[ *.EVT\_UCX\_终结点\_确定\_以\_取消\_的传输*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)  
通知控制器驱动程序它可以在终结点上完成已取消的传输。

[ *\_\_\_的*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_purge)  
在终结点上完成所有未完成的 i/o 请求。

[ *\_UCX\_终结点\_开始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_start)  
启动与终结点关联的队列。

[ *.EVT\_UCX\_终结点\_静态\_流\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)  
创建静态流。

[ *\_重置\_\_的 .EVT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_reset)  
通知驱动程序重置控制器的终结点编程。

当主机控制器驱动程序在终结点上收到 USB 3.0 无 Ping 响应错误时，驱动程序必须调用[**UcxEndpointNoPingResponseError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointnopingresponseerror)。 该调用会导致接收 .Evt 的 USB 设备对象[ *\_UCX\_USBDEVICE\_更新*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_update)。
有关详细信息，请参阅[在主机控制器驱动程序中配置 USB 端点](configuring-usb-endpoints-in-a-host-controller-driver.md)。

## <a name="stream-object"></a>Stream 对象


**UCXSTREAMS**

表示单个终结点到设备的多个管道。 主机控制器驱动程序在[ *\_UCX\_终结点\_静态\_流*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)中创建流对象，\_通过调用[**UcxStaticStreamsCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)来添加回调。

在[**UcxStaticStreamsCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)调用期间，主机控制器驱动程序将注册其回调函数。 对于特定的终结点对象，驱动程序可以确定它是否已创建流对象，并通过调用[**UcxEndpointGetStaticStreamsReferenced**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointgetstaticstreamsreferenced)返回 UCXSTREAMS 句柄。

创建对象后，驱动程序将为每个流创建一个框架队列对象，并通过调用[**UcxStaticStreamsSetStreamInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamssetstreaminfo)将 WDFQUEUE 句柄发送到 UCX。

Stream 对象为主机控制器提供了若干回调函数，以帮助 UCX 管理静态流。

[ *.EVT\_UCX\_终结点\_静态\_流\_禁用*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_disable)  
为终结点的所有流释放控制器资源。

[ *.EVT\_UCX\_终结点\_静态\_流\_启用*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_enable)  
为此终结点启用所有流的控制器硬件。

对象的生存期和关联的队列由 UCX 管理，驱动程序不能删除这些对象。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)  



