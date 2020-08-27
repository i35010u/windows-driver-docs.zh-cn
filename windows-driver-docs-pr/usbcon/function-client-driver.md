---
description: 介绍函数控制器客户端驱动程序在与 USB 函数控制器扩展)  (UFX 时执行的各种任务。
title: 编写函数控制器客户端驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f64501cc3adcc0a6d36460c205461b1c13d8bad4
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969394"
---
# <a name="write-a-function-controller-client-driver"></a>编写函数控制器客户端驱动程序


**摘要**

-   描述函数控制器客户端驱动程序的预期行为。

**适用于**

-   Windows 10
-   为 USB 设备编写控制器驱动程序的驱动程序开发人员

**重要的 API**

-   [USB 函数控制器客户端驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usb-function-controller-client-driver-reference)


介绍函数控制器客户端驱动程序在与 USB 函数控制器扩展)  (UFX 时执行的各种任务。 UFX 和客户端驱动程序使用导出方法和事件回调函数相互通信。 名为 **UfxDeviceXxx** 或 **UfxEndpointXxx**)  (的导出方法由 UFX 导出并由客户端驱动程序调用。 在客户端驱动程序中实现名为 *.Evt \_ UFX \_ Xxx*)  (回调函数并由 UFX 调用。

UFX 异步调用所有客户端驱动程序的回调函数，每个对象一次调用一个回调。 例如，有一个 USB 设备对象和三个终结点对象。 对于一个设备，最多有四个回调函数 (一个，每次可以调用一个) 。 对于每个回调方法，UFX 将一直等待，直到客户端驱动程序调用 [**UfxDeviceEventComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete) ，以指示驱动程序已完成该请求。 等待这些导出的同时，UFX 侦听的其他导出方法为 [**UfxDeviceNotifyHardwareFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwarefailure)。 许多客户端回调函数是可选的。 必需的函数如下所示：

-   [*.EVT \_ UFX \_ 设备 \_ 默认 \_ 终结点 \_ 添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)
-   [*.EVT \_ UFX \_ 设备 \_ 终结点 \_ 添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)
-   [*.EVT \_ UFX \_ 设备 \_ 主机 \_ 连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)
-   [*.EVT \_ UFX \_ 设备 \_ 主机 \_ 断开连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)
-   [*.EVT \_ UFX \_ 设备 \_ 寻址*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_addressed)

## <a name="initialization"></a>初始化


1.  当 Windows Driver Foundation (WDF) 调用客户端驱动程序的 [**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调实现时，函数控制器客户端驱动程序将启动初始化过程。 在该实现中，客户端驱动程序应调用 [**UfxFdoInit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxfdoinit) ，然后通过调用 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建设备对象。
2.  客户端驱动程序调用 [**UfxDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicecreate) 来创建 USB 设备对象并检索 UFXDEVICE 句柄。
3.  客户端驱动程序调用 [**UfxDeviceNotifyHardwareReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwareready) ，以指示 UFX 它现在可以调用客户端驱动程序的回调函数。
4.  UFX 执行如下初始化任务：
    -   UFX 调用客户端驱动程序的 [*.Evt \_ UFX \_ 设备 \_ 默认 \_ 终结点 \_ 添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add) 实现来创建默认终结点。
    -   对于设备支持的接口，UFX 创建 (PDOs) 的子物理设备对象。
    -   UFX 在发送 [**IOCTL \_ 内部 \_ USBFN \_ ACTIVATE \_ USB \_ 总线**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_activate_usb_bus) 请求时等待设备类驱动程序激活。 它还会等待客户端驱动程序调用 [**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach) ，指出设备已附加。

## <a name="class-driver-notification"></a>类驱动程序通知


为了获得有关安装包的通知以及总线的状态，类驱动程序应发送 [**IOCTL \_ 内部 \_ USBFN \_ 激活 \_ USB \_ 总线**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_activate_usb_bus) 请求。 UFX 将这些请求排队到类驱动程序特定的通知队列。 收到来自客户端驱动程序的总线事件的通知后，UFX 会从每个适当的队列中弹出，并完成该请求。 为了防止类驱动程序缺失通知，UFX 为类驱动程序保留固定大小的通知队列。

## <a name="device-attach-and-detach-events"></a>设备附加和分离事件


UFX 假定设备已分离，直到其成为函数控制器客户端驱动程序调用 [**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach)。

在该调用后，UFX 将设备状态设置为 USB 规范中定义的 "已 **启动** "。 若要通知客户端驱动程序的状态更改，UFX 会调用客户端驱动程序的 [*.Evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) 实现。

UFX 通知充电器驱动程序 ( # A0) 帮助对设备充电。 UFX 还通过完成类驱动程序以前发送的 [**IOCTL \_ 内部 \_ USBFN \_ 总线 \_ 事件 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification) 请求，通知类驱动程序。

当分离总线时，客户端驱动程序必须调用 [**UfxDeviceNotifyDetach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifydetach) 。 客户端在每次调用 [**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach)后，只能调用一次分离。 **UfxDeviceNotifyDetach**调用后，如果这不是) 的接口更改，则 UFX 将调用[*.Evt \_ UFX \_ 设备 \_ 主机 \_ 断开连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect) (。 然后，UFX 将继续执行所有清理任务，如清除所有终结点队列和启动默认终结点队列。 UFX 调用 [*.Evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) ，并通过完成 [**IOCTL \_ 内部 \_ USBFN \_ 总线 \_ 事件 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification) 请求来通知类驱动程序。

**硬件故障**

如果发生硬件错误，则客户端驱动程序应调用 [**UfxDeviceNotifyHardwareFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwarefailure)。 在响应中，UFX 将会关闭设备堆栈，并可能会通过调用客户端驱动程序的 [*.Evt \_ UFX \_ 设备 \_ 控制器 \_ 重置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_controller_reset)，尝试从这种情况中恢复。 客户端应将控制器重置为其初始状态。 如果发生其他硬件故障，客户端应再次调用 UfxDeviceNotifyHardwareFailure。 在第二次调用时，UFX 将记录其状态和 bug 检查。

## <a name="port-detection"></a>端口检测


端口检测由 UFX 执行。 它调用函数控制器客户端驱动程序 [*的 \_ UFX \_ 设备 \_ 端口 \_ 检测*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_detect) 回调函数来确定设备连接到的端口类型。 客户端通过使用[**USBFN \_ 端口 \_ 类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_port_type)中定义的一个端口类型调用[**UfxDevicePortDetectComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceportdetectcomplete)或[**UfxDevicePortDetectCompleteEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceportdetectcompleteex)来做出响应。

如果客户端无法确定端口类型，客户端应报告 **UsbfnUnknownPort**。 如果端口未知或下游端口，UFX 将调用客户端驱动程序的 [* \_ UFX \_ 设备 \_ 主机 \_ 连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect) 功能。 UFX 侦听总线一段时间。 如果端口未知，但存在流量，如安装包，则 UFX 将采用 **UsbfnStandardDownstreamPort**。 否则，UFX 会将端口分配给 **UsbfnInvalidDedicatedChargingPort**。 确定端口类型后，UFX 会通知 Cad.sys 并调用客户端驱动程序的 [*.Evt \_ UFX \_ 设备 \_ 端口 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change) 功能。 在函数中，客户端驱动程序需要更改硬件状态以匹配 UFX 端口类型。

## <a name="endpoint-creation"></a>终结点创建


UFX 通过调用客户端驱动程序的 [*.Evt \_ UFX \_ 设备 \_ 默认 \_ 终结点 \_ 添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add) (终结点 0) 创建默认终结点，以便能够处理主机发送的安装包。 UFX 通过调用 [*.Evt \_ UFX \_ 设备 \_ 终结点 \_ 添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)创建其他终结点。 UFX 仅在客户端驱动程序调用 [**UfxDeviceNotifyHardwareReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwareready)后创建终结点。 在这些回调函数中，客户端驱动程序应向终结点对象调用 [**UfxEndpointCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointcreate) ，并获取其 UFXENDPOINT 句柄。 UFX 将父项设置为与终结点所属的接口关联的类驱动程序 PDO。 默认终结点的父项是 USB 设备对象。 终结点包含两个框架队列对象：传输队列和命令队列，这两个对象都只能在设备处于配置状态时进行访问， (终结点0，在 UFX 调用 [*.Evt \_ UFX \_ 设备 \_ 主机 \_ 连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)) 后，可以访问该队列。

-   **命令队列请求**
-   [**IOCTL \_ 内部 \_ USBFN \_ 获取 \_ 管道 \_ 状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_get_pipe_state)
-   [**IOCTL \_ 内部 \_ USBFN \_ 设置 \_ 管道 \_ 状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)
-   [**IOCTL \_ 内部 \_ USBFN \_ 描述符 \_ 更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)
-   **传输队列请求**
-   [**IOCTL \_ 内部 \_ USBFN \_ 传输 \_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)
-   [**\_ \_ \_ \_ \_ 追加 \_ 零 \_ PKT 中的 IOCTL 内部 USBFN 传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)
-   [**IOCTL \_ 内部 \_ USBFN \_ 传出 \_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)
-   [**IOCTL \_ 内部 \_ USBFN \_ 控制 \_ 状态 \_ 握手 \_ IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_in)
-   [**IOCTL \_ 内部 \_ USBFN \_ 控制 \_ 状态 \_ 握手 \_ 输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_out)

## <a name="device-enumeration"></a>设备枚举


在 UFX 调用驱动程序的 [*.Evt \_ UFX \_ 设备 \_ 主机 \_ 连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)之前，客户端驱动程序不应允许连接到主机。 当客户端驱动程序调用 [**UfxDeviceNotifyReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyreset)时，将开始设备枚举。 **默认**状态下，UFX 处理标准安装包。

**重置**

UFX 清除所有终结点队列，并向客户端驱动程序发送 [**IOCTL \_ 内部 \_ USBFN \_ 描述符 \_ 更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update) 请求，以更新终结点0的 **wMaxPacketSize** 。 UFX 启动默认终结点的队列，并将状态设置为 **默认值**。

**默认**

UFX 调用客户端驱动程序的 [*.Evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) 功能。 它还通知类驱动程序状态。 UFX 接收到设置 \_ 地址标准安装包后，UFX 会将状态设置为 "已 **解决**"。

**解除**

UFX 调用客户端驱动程序的 [*.Evt \_ UFX \_ 设备 \_ 寻址*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_addressed) 函数向客户端指示应使用的地址。 -如果地址为0，则 UFX 会将状态设置回 **默认值** ，并调用 [*.Evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) 并通知类驱动程序。 接收到设置 \_ 配置标准安装包后，UFX 会将状态设置为 " **已配置**"。

**已配置**

如果所选配置为0，则 UFX 将清除接口终结点，并将状态设置为 "已 **解决**"。 UFX 将 [**IOCTL \_ 内部 \_ USBFN \_ 描述符 \_ 更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update) 请求发送到客户端驱动程序，以更新接口终结点的 **wMaxPacketSize** 。 UFX 确保所有接口终结点队列已完成清除和启动接口终结点队列。 如果端口类型不是 **UsbfnStandardDownstreamPort** 或 **UsbfnChargingDownstreamPort**，则 UFX 会将端口类型更改为 **UsbfnStandardDownstreamPort** 并通知 Cad.sys;客户端驱动程序，方法是调用 [*.Evt \_ UFX \_ 设备 \_ 端口 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change) ，并使用 [*.evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) 来更新状态; 已配置状态的类驱动程序。

## <a name="standard-control-transfers"></a>标准控制传输


UFX 可以在调用由客户端驱动程序使用创建的默认终结点后，随时处理默认终结点上的控制传输。 [* \_ \_ \_ \_ \_ *](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add) 所有控制传输均以8字节安装包开始。 若要将安装数据包发送到主机，客户端驱动程序应调用 [**UfxEndpointNotifySetup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointnotifysetup)。 标准控制传输由 UFX 完成。 如果存在与控件传输相关联的数据，UFX 会根据需要读取和写入默认控制终结点。

## <a name="non-standard-control-transfers"></a>非标准控制传输


如果 UFX 无法处理控件传输，则通过完成 [**IOCTL \_ 内部 \_ USBFN \_ BUS \_ 事件 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification) 请求，将传输转发到相应的类驱动程序。 在终结点描述符中定义为控制终结点的任何终结点上，都可以进行控件传输。 除默认控制终结点以外的其他终结点上的控制传输总是非标准的控件传输。 如果控制终结点是默认控制终结点，则 UFX 将通知安装包的类驱动程序，这些包标记为该类驱动程序的类请求。 如果控制终结点属于某个接口，则 UFX 将通知与该接口关联的类驱动程序。 如有必要，类驱动程序应读取并写入控制终结点。

## <a name="data-transfers"></a>数据传输


数据传输由类驱动程序通过 [** \_ \_ \_ \_ 在中发送 ioctl 内部 USBFN 传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)、 [**在 \_ \_ \_ \_ \_ 追加 \_ 零 \_ PKT 中的 ioctl 内部 USBFN 传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)或 [**ioctl \_ 内部 \_ USBFN \_ 传出 \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out) 请求启动。 验证每个请求后，UFX 会将其转发到相应的终结点队列，以供客户端驱动程序处理。 客户端驱动程序应执行其他验证。 客户端驱动程序在终结点队列上接收传输请求。 客户端驱动程序可以检索此队列的多个请求，因为它需要最大限度地提高总线使用率。 客户端驱动程序应完成成功的请求，状态为 " \_ 成功"。 该驱动程序应该尽力尝试取消请求，并完成取消的状态为 "已取消" 的请求 \_ 。 如果传递的参数无效，则客户端驱动程序将完成请求，状态为 \_ 无效 \_ 参数。

**控制传输**

控件传输始于8字节安装包。 若要将安装数据包发送到主机，客户端驱动程序应调用 [**UfxEndpointNotifySetup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointnotifysetup)。 UFX 通过完成通知请求通知非标准控件传输的类驱动程序。 客户端和 UFX 都使用 [**ioctl \_ 内部 \_ USBFN \_ 传输 \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)，在 [** \_ \_ \_ \_ \_ 追加 \_ 零 \_ PKT 中使用 ioctl 内部 USBFN 传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)，或使用 [**ioctl \_ 内部 \_ USBFN \_ 传出 \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out) 来读取和写入默认控制终结点。 但是，接口可以定义其他控件终结点，这些终结点只有相应的类驱动程序才能使用。 控制终结点可能会停止响应安装包。 类驱动程序会将 [**IOCTL \_ 内部 \_ USBFN \_ 设置 \_ 管道 \_ 状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state) 请求发送到终结点。 在发送延迟后，硬件或客户端驱动程序应立即在终结点上恢复流量。 控制终结点还可以发送和接收长度为零的数据包 (ZLP) ，无需任何以前的数据。 客户端驱动程序和 UFX 可以通过使用 [**中的 ioctl \_ 内部 \_ USBFN \_ 控制 \_ 状态 \_ 握手 \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_in) 和 [**ioctl \_ 内部 \_ USBFN \_ 控制 \_ 状态 \_ 握手 \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_out)来实现此目的。

**大容量和中断传输**

批量传输可保证数据的传送，并用于发送大量数据。 可以在 [**中使用 ioctl \_ 内部 \_ USBFN \_ 传输、 \_ 在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in) [** \_ \_ \_ \_ \_ 追加 \_ 零 \_ PKT 中的 ioctl 内部 USBFN 传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)或 [**ioctl \_ 内部 \_ USBFN \_ \_ 外**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)传输，在批量终结点上发送传输。 使用 [**IOCTL \_ 内部 \_ USBFN \_ 设置 \_ 管道 \_ 状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)控制终结点时，大容量终结点可能会停止。 客户端驱动程序应发送一个延迟数据包，以响应所有主机请求并保留 IOCTL 请求。 与控制终结点不同，已停止的大容量终结点将保持停止状态，直到显式清除该延迟状态。

中断传输中断传输类似于大容量传输，但有一定的延迟。 中断传输与大容量传输具有相同的接口，但没有流式处理功能。

**同步传输**

在此版本中，客户端驱动程序不应支持同步传输。

## <a name="power-management"></a>电源管理


客户端驱动程序拥有电源管理的所有方面。 由于回调函数是异步的，因此，客户端驱动程序应返回到适当的电源状态，并在调用适当的事件完成导出函数之前完成请求，如 [**UfxDeviceEventComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)。

如果设备状态 (在 [**USBFN \_ 设备 \_ 状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_device_state) 中定义) 为 **UsbfnDeviceStateSuspended** 和 **UsbfnDeviceStateAttached**，并且未报告端口类型，则 UFX 处于工作状态。 或者，UFX 报告了端口类型 (在 [**USBFN \_ 端口 \_ 类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_port_type)) **UsbfnStandardDownstreamPort** 或 **UsbfnChargingDownstreamPort**中定义。

UFX 进入并退出工作状态，方法是调用 [*.Evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) 或 [*.evt \_ UFX \_ 设备 \_ 端口 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change) 实现。 当客户端驱动程序调用 [**UfxDeviceEventComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)时，与工作状态之间的转换完成。

在工作状态下，UFX 可以调用任何回调。 当不处于工作状态时，UFX 只会调用 [*.Evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) 来进入工作状态; [*.Evt \_UFX \_ 设备 \_ 远程 \_ 唤醒 \_ 信号*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_remote_wakeup_signal) ，在挂起 (期间发出远程唤醒（如果支持) ）。

**设备暂停**

如果总线上没有流量3毫秒，则会发生设备暂停。 在这种情况下，客户端驱动程序必须在通过调用 [**UfxDeviceNotifySuspend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifysuspend) 和 [**UfxDeviceNotifyResume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyresume)检测到挂起和恢复时，通知 UFX。 接收这些调用后，UFX [*将调用 .Evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) ，并通过完成 [**IOCTL \_ 内部 \_ USBFN \_ 总线 \_ 事件 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification) 请求通知类驱动程序。 如果设备支持远程唤醒，并且主机启用了远程唤醒，则 UFX 可能会在挂起时调用 *.Evt \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改* ，以发出远程唤醒信号。

## <a name="related-topics"></a>相关主题
[Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)  
[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)  
[USB 功能客户端驱动程序使用的 UFX 对象和句柄](ufx-objects-and-handles-used-by-a-usb-function-controller.md)  



