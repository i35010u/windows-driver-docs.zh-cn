---
Description: 介绍函数控制器客户端驱动程序在与 USB 函数控制器扩展（UFX）交互时执行的各种任务。
title: 编写函数控制器客户端驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 240cbb5aa16c88545795fac8d1488729af3451b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845004"
---
# <a name="write-a-function-controller-client-driver"></a>编写函数控制器客户端驱动程序


**摘要**

-   描述函数控制器客户端驱动程序的预期行为。

**适用于**

-   Windows 10
-   为 USB 设备编写控制器驱动程序的驱动程序开发人员

**重要的 API**

-   [USB 函数控制器客户端驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usb-function-controller-client-driver-reference)


介绍函数控制器客户端驱动程序在与 USB 函数控制器扩展（UFX）交互时执行的各种任务。 UFX 和客户端驱动程序使用导出方法和事件回调函数相互通信。 导出方法（名为**UfxDeviceXxx**或**UFXENDPOINTXXX**）由 UFX 导出并由客户端驱动程序调用。 回调函数（名为 *.evt\_UFX\_Xxx*）在客户端驱动程序中实现并由 UFX 调用。

UFX 异步调用所有客户端驱动程序的回调函数，每个对象一次调用一个回调。 例如，有一个 USB 设备对象和三个终结点对象。 一次只能调用四个回调函数（一个用于设备，一个用于每个终结点）。 对于每个回调方法，UFX 将一直等待，直到客户端驱动程序调用[**UfxDeviceEventComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete) ，以指示驱动程序已完成该请求。 等待这些导出的同时，UFX 侦听的其他导出方法为[**UfxDeviceNotifyHardwareFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwarefailure)。 许多客户端回调函数是可选的。 必需的函数如下所示：

-   [ *.EVT\_UFX\_设备\_默认\_终结点\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)
-   [ *\_设备\_\_的 .EVT\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)
-   [ *.EVT\_UFX\_设备\_主机\_连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)
-   [ *.EVT\_UFX\_设备\_主机\_断开连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)
-   [ *\_设备\_的\_UFX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_addressed)

## <a name="initialization"></a>初始化


1.  当 Windows Driver Foundation （WDF）调用客户端驱动程序的[**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调实现时，函数控制器客户端驱动程序将启动初始化过程。 在该实现中，客户端驱动程序应调用[**UfxFdoInit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxfdoinit) ，然后通过调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建设备对象。
2.  客户端驱动程序调用[**UfxDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicecreate)来创建 USB 设备对象并检索 UFXDEVICE 句柄。
3.  客户端驱动程序调用[**UfxDeviceNotifyHardwareReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwareready) ，以指示 UFX 它现在可以调用客户端驱动程序的回调函数。
4.  UFX 执行如下初始化任务：
    -   UFX 调用客户端驱动程序的[ *.evt\_UFX\_设备\_默认\_终结点\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)实现来创建默认终结点。
    -   UFX 为设备支持的接口创建子物理设备对象（PDOs）。
    -   UFX 在发送[**IOCTL\_内部\_USBFN\_激活\_USB\_总线**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_activate_usb_bus)请求时，等待设备类驱动程序激活。 它还会等待客户端驱动程序调用[**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach) ，指出设备已附加。

## <a name="class-driver-notification"></a>类驱动程序通知


为了获得有关安装包的通知和总线的状态，类驱动程序应发送[**IOCTL\_内部\_USBFN\_激活\_USB\_总线**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_activate_usb_bus)请求。 UFX 将这些请求排队到类驱动程序特定的通知队列。 收到来自客户端驱动程序的总线事件的通知后，UFX 会从每个适当的队列中弹出，并完成该请求。 为了防止类驱动程序缺失通知，UFX 为类驱动程序保留固定大小的通知队列。

## <a name="device-attach-and-detach-events"></a>设备附加和分离事件


UFX 假定设备已分离，直到其成为函数控制器客户端驱动程序调用[**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach)。

在该调用后，UFX 将设备状态设置为 USB 规范中定义的 "已**启动**"。 若要通知客户端驱动程序的状态更改，UFX 会调用客户端驱动程序的[ *\_UFX\_设备\_USB\_状态\_更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)实现。

UFX 通知充电器驱动程序（http.sys）有助于对设备进行收费。 UFX 还会通过完成[**IOCTL\_内部\_USBFN\_总线\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)来通知类驱动程序，\_类驱动程序以前发送的通知请求。

当分离总线时，客户端驱动程序必须调用[**UfxDeviceNotifyDetach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifydetach) 。 客户端在每次调用[**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach)后，只能调用一次分离。 在**UfxDeviceNotifyDetach**调用后，UFX 会调用[ *\_UFX\_设备\_主机\_断开连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)（如果这不是接口更改）。 然后，UFX 将继续执行所有清理任务，如清除所有终结点队列和启动默认终结点队列。 UFX 调用[ *\_UFX\_设备\_USB\_状态\_更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)并通过完成[**IOCTL\_内部\_USBFN\_BUS\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)来通知类驱动程序发出.

**硬件故障**

如果发生硬件错误，则客户端驱动程序应调用[**UfxDeviceNotifyHardwareFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwarefailure)。 作为响应，UFX 将从设备堆栈中拆下，并通过调用客户端驱动程序的[ *\_UFX\_设备\_控制器\_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_controller_reset)来尝试从这种情况下恢复。 客户端应将控制器重置为其初始状态。 如果发生其他硬件故障，客户端应再次调用 UfxDeviceNotifyHardwareFailure。 在第二次调用时，UFX 将记录其状态和 bug 检查。

## <a name="port-detection"></a>端口检测


端口检测由 UFX 执行。 它调用函数控制器客户端驱动程序的[ *.evt\_UFX\_device\_端口\_检测*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_detect)回调函数来确定设备连接到的端口类型。 客户端通过使用[**USBFN\_端口\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_port_type)中定义的某个端口类型调用[**UfxDevicePortDetectComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceportdetectcomplete)或[**UfxDevicePortDetectCompleteEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceportdetectcompleteex)来做出响应。

如果客户端无法确定端口类型，客户端应报告**UsbfnUnknownPort**。 如果端口未知或下游端口，则 UFX 会调用客户端驱动程序的[ *\_UFX\_设备\_主机\_连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)功能。 UFX 侦听总线一段时间。 如果端口未知，但存在流量，如安装包，则 UFX 将采用**UsbfnStandardDownstreamPort**。 否则，UFX 会将端口分配给**UsbfnInvalidDedicatedChargingPort**。 确定端口类型后，UFX 会通知，并调用客户端驱动程序的[ *.evt\_UFX\_设备\_端口\_CHANGE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change)函数。 在函数中，客户端驱动程序需要更改硬件状态以匹配 UFX 端口类型。

## <a name="endpoint-creation"></a>终结点创建


UFX 通过调用客户端驱动程序的[ *\_UFX\_设备\_默认\_终结点*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)来创建默认终结点（终结点0），\_添加，使其能够处理主机发送的安装包。 UFX 通过[ *\_调用\_设备\_终结点\_"添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)" 来创建其他终结点。 UFX 仅在客户端驱动程序调用[**UfxDeviceNotifyHardwareReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwareready)后创建终结点。 在这些回调函数中，客户端驱动程序应向终结点对象调用[**UfxEndpointCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointcreate) ，并获取其 UFXENDPOINT 句柄。 UFX 将父项设置为与终结点所属的接口关联的类驱动程序 PDO。 默认终结点的父项是 USB 设备对象。 终结点包含两个框架队列对象：传输队列和命令队列，这两个对象都只能在设备处于配置状态时访问（终结点0除外，可在 UFX 调用\_UFX 之后访问该终结点） [ *\_设备\_主机\_连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)）。

-   **命令队列请求**
-   [**IOCTL\_内部\_USBFN\_获取\_管道\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_get_pipe_state)
-   [**IOCTL\_内部\_USBFN\_设置\_管道\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)
-   [**IOCTL\_内部\_USBFN\_描述符\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)
-   **传输队列请求**
-   [**IOCTL\_内部\_USBFN\_传输\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)
-   [**IOCTL\_内部\_USBFN\_传输\_\_追加\_零\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)
-   [**IOCTL\_内部\_USBFN\_传输\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)
-   [**IOCTL\_内部\_USBFN\_控件\_状态\_握手\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_in)
-   [**IOCTL\_内部\_USBFN\_控件\_状态\_握手\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_out)

## <a name="device-enumeration"></a>设备枚举


在[ *\_UFX\_设备\_主机\_连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)之前，客户端驱动程序不应允许连接到主机。 当客户端驱动程序调用[**UfxDeviceNotifyReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyreset)时，将开始设备枚举。 **默认**状态下，UFX 处理标准安装包。

**重置**

UFX 清除所有终结点队列，并向客户端驱动程序发送[**IOCTL\_内部\_USBFN\_描述符\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)请求，以更新终结点0的**wMaxPacketSize** 。 UFX 启动默认终结点的队列，并将状态设置为**默认值**。

**缺省值**

UFX 调用客户端驱动程序的[ *\_UFX\_设备\_USB\_状态\_CHANGE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)函数。 它还通知类驱动程序状态。 UFX 接收到\_地址标准安装包的集合后，UFX 会将状态设置为 "已**解决**"。

**解除**

UFX 调用客户端驱动程序的[ *.evt\_UFX\_设备\_寻址*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_addressed)的函数向客户端指明应使用的地址。 -如果地址为0，则 UFX 会将状态设置回**默认值**，并[ *\_UFX\_设备\_USB\_状态\_更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)并通知类驱动程序。 接收到\_配置标准安装包的集合时，UFX 会将状态设置为 "**已配置**"。

**尚未**

如果所选配置为0，则 UFX 将清除接口终结点，并将状态设置为 "已**解决**"。 UFX 将[**IOCTL\_内部\_USBFN\_描述符\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)请求发送到客户端驱动程序，以更新接口终结点的**wMaxPacketSize** 。 UFX 确保所有接口终结点队列已完成清除和启动接口终结点队列。 如果端口类型不是**UsbfnStandardDownstreamPort**或**UsbfnChargingDownstreamPort**，则 UFX 会将端口类型更改为**UsbfnStandardDownstreamPort**并通知。客户端驱动程序：通过调用[ *\_UFX\_设备\_端口\_更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change)和[ *.evt\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)\_\_\_\_已配置状态的类驱动程序。

## <a name="standard-control-transfers"></a>标准控制传输


UFX 可以随时处理默认终结点上的控制传输[ *\_UFX\_设备\_默认\_终结点\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)，其中客户端驱动程序使用创建默认终结点。 所有控制传输均以8字节安装包开始。 若要将安装数据包发送到主机，客户端驱动程序应调用[**UfxEndpointNotifySetup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointnotifysetup)。 标准控制传输由 UFX 完成。 如果存在与控件传输相关联的数据，UFX 会根据需要读取和写入默认控制终结点。

## <a name="non-standard-control-transfers"></a>非标准控制传输


如果 UFX 无法处理控件传输，则会通过完成[**IOCTL\_内部\_USBFN\_总线\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)请求，将传输转发到相应的类驱动程序。 在终结点描述符中定义为控制终结点的任何终结点上，都可以进行控件传输。 除默认控制终结点以外的其他终结点上的控制传输总是非标准的控件传输。 如果控制终结点是默认控制终结点，则 UFX 将通知安装包的类驱动程序，这些包标记为该类驱动程序的类请求。 如果控制终结点属于某个接口，则 UFX 将通知与该接口关联的类驱动程序。 如有必要，类驱动程序应读取并写入控制终结点。

## <a name="data-transfers"></a>数据传输


数据传输是由类驱动程序通过[**在中发送 ioctl\_内部\_USBFN\_传输\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)来启动的， [**IOCTL\_内部\_USBFN\_在\_追加\_零\_传输\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)或[**IOCTL\_内部\_USBFN\_传输\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)请求。 验证每个请求后，UFX 会将其转发到相应的终结点队列，以供客户端驱动程序处理。 客户端驱动程序应执行其他验证。 客户端驱动程序在终结点队列上接收传输请求。 客户端驱动程序可以检索此队列的多个请求，因为它需要最大限度地提高总线使用率。 客户端驱动程序应完成成功请求，状态\_成功。 该驱动程序应该尽力尝试取消请求，并完成取消\_状态的已取消请求（如果已取消）。 如果传递的参数无效，则客户端驱动程序将完成请求，状态\_无效\_参数。

**控制传输**

控件传输始于8字节安装包。 若要将安装数据包发送到主机，客户端驱动程序应调用[**UfxEndpointNotifySetup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointnotifysetup)。 UFX 通过完成通知请求通知非标准控件传输的类驱动程序。 客户端和 UFX 都使用[**ioctl\_内部\_USBFN\_传输\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)， [**IOCTL\_内部\_USBFN\_在\_追加\_零\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)或[**IOCTL\_内部\_USBFN\_传输\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out) ，以读取和写入默认控制终结点。 但是，接口可以定义其他控件终结点，这些终结点只有相应的类驱动程序才能使用。 控制终结点可能会停止响应安装包。 类驱动程序将[**IOCTL 发送\_内部\_USBFN\_将\_管道\_状态请求设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)为延迟终结点。 在发送延迟后，硬件或客户端驱动程序应立即在终结点上恢复流量。 控制终结点还可以发送和接收长度为零的数据包（ZLP），而无需任何以前的数据。 客户端驱动程序和 UFX 可以通过使用[**ioctl\_内部\_USBFN\_控件\_状态\_握手**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_in)\_和[**IOCTL\_内部\_USBFN\_控件\_状态\_握手\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_out)。

**大容量和中断传输**

批量传输可保证数据的传送，并用于发送大量数据。 可以使用 Ioctl 在大容量终结点上发送传输[ **\_内部\_USBFN\_传输\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)， [**IOCTL\_内部\_USBFN\_传输\_\_追加\_零\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)或[**IOCTL\_内部\_USBFN\_传输\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)。 大容量终结点可能停止使用[**IOCTL\_内部\_USBFN\_\_管道\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)来控制终结点。 客户端驱动程序应发送一个延迟数据包，以响应所有主机请求并保留 IOCTL 请求。 与控制终结点不同，已停止的大容量终结点将保持停止状态，直到显式清除该延迟状态。

中断传输中断传输类似于大容量传输，但有一定的延迟。 中断传输与大容量传输具有相同的接口，但没有流式处理功能。

**同步传输**

在此版本中，客户端驱动程序不应支持同步传输。

## <a name="power-management"></a>电源管理


客户端驱动程序拥有电源管理的所有方面。 由于回调函数是异步的，因此，客户端驱动程序应返回到适当的电源状态，并在调用适当的事件完成导出函数之前完成请求，如[**UfxDeviceEventComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)。

如果设备状态（在[**USBFN\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_device_state)中定义）为**UsbfnDeviceStateSuspended**和**UsbfnDeviceStateAttached**并且未报告端口类型，则 UFX 处于工作状态。 或者，UFX 报告了端口类型（在[**USBFN\_端口\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_port_type)） **UsbfnStandardDownstreamPort**或**UsbfnChargingDownstreamPort**中定义。

UFX 进入并退出工作状态，方法是： [ *\_设备\_USB\_状态\_更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)或[ *.evt\_UFX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change)\_\_\_更改实现中调用\_。 当客户端驱动程序调用[**UfxDeviceEventComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)时，与工作状态之间的转换完成。

在工作状态下，UFX 可以调用任何回调。 当不处于工作状态时，UFX 只会调用[ *\_设备\_USB\_\_状态\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)[ *.Evt\_UFX\_设备\_远程\_唤醒\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_remote_wakeup_signal)在挂起期间发出远程唤醒的信号（如果支持）。

**设备暂停**

如果总线上没有流量3毫秒，则会发生设备暂停。 在这种情况下，客户端驱动程序必须在通过调用[**UfxDeviceNotifySuspend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifysuspend)和[**UfxDeviceNotifyResume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyresume)检测到挂起和恢复时，通知 UFX。 接收到这些调用后，\_UFX 会[ *\_设备\_USB\_状态\_更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)并通知类驱动程序，方法是在接收这些调用时，通过完成[**IOCTL\_内部\_USBFN\_BUS\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)请求。 如果设备支持远程唤醒，并且主机启用了远程唤醒，UFX 可能会调用 *\_设备\_USB\_\_状态*的调用\_

## <a name="related-topics"></a>相关主题
[Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)  
[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)  
[UFX USB 函数客户端驱动程序使用的对象和句柄](ufx-objects-and-handles-used-by-a-usb-function-controller.md)  



