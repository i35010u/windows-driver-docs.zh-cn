---
description: 用于发送 MA USB 数据包的 USB 设备驱动程序。
title: 不区分媒体的 (MA-USB) 协议的客户端驱动程序
ms.date: 09/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff44007e6d1b7a459a9c3aae1d15cdc3f513bd83
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009975"
---
# <a name="usb-client-drivers-for-media-agnostic-ma-usb"></a>不区分媒体的 (MA-USB) 协议的客户端驱动程序

在 Windows 10 中，版本1709中，USB 驱动程序堆栈可以通过使用不可知的 USB (MA-USB) 协议，通过非 USB 物理介质（例如 Wi-fi）发送 USB 数据包。 新功能的设计方式是使现有 USB 客户端驱动程序所需的更改降到最低。 这组更改包括有关传输的其他信息：

-   对于具有同步或流式处理终结点的设备，客户端驱动程序需要知道与传输编程和传输完成相关的延迟，以便驱动程序可以确保设备在时间获取同步数据包。

-   客户端驱动程序可以使用该 informationf 来优化更高层的协议选择。 例如，显示驱动程序可以使用延迟和带宽信息来选择最佳编解码器和缓冲方案。 由于这些特征可能会动态更改，因此驱动程序需要确定更改。

## <a name="getting-the-delays-for-isochronous-transfers"></a>获取同步传输延迟

对于同步终结点，客户端驱动程序需要了解最大编程延迟和最大完成延迟时间。 该请求必须针对特定管道，因为同一设备上的不同终结点的延迟可能不同，因为 MA-USB 规范为主机提供了计算这些值的机制。 

若要生成该请求，驱动程序必须使用 **_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS** URB。

> [!NOTE]
> 在此版本中，此功能仅适用于 KMDF 和基于 WDM 的驱动程序。 

下面是一些用于生成此 URB 的最佳做法：


-    客户端 dirver 必须通过调用 [WdfUsbTargetDeviceCreateUrb](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb) 或 [USBD_UrbAllocate](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)来分配此 URB。 
- 可以在 <= 调度级别发送 URB。
- 如果 URB 的目标是非同步终结点，则 USB 驱动程序堆栈将无法请求。
- 客户端驱动程序不得假设第三方 USB 堆栈支持此 URB。 它将受所有 Microsoft = 提供的收件箱 USB 客户端驱动程序的支持。

对于流式处理中的连续同步，客户端驱动程序通常会发出多个未处理的读取请求。 驱动程序可以使用往返时间来计算需要基于未处理的读取请求数的读取请求中的同步数据包的数量。

例如，如果未处理的请求数为二，则 URB 中的同步数据包数应至少为 (总往返时间) / (时间间隔) ，其中总往返时间 = MaximumSendPathDelayInMilliSeconds + MaximumCompletionPathDelayInMilliSeconds

如果发送延迟 = 10 毫秒，则完成延迟 = 15msec，then 总往返次数 = 25msec。
如果服务间隔的长度 = 5 毫秒（对于连续流式处理，则为 URBs = 2），则每个按下的 URBs 中的同步数据包数应至少为 = 25/5 = 5 的数据包。

## <a name="getting-the-host-controller-transport-characteristics"></a>获取主机控制器传输特性
客户端驱动程序可以通过发送以下 IOCTLs 请求来检索传输特征：

-    [IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics)
-    [IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change)
-    [IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change) 
-    [IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)

由于 USB 驱动程序堆栈依赖于基础传输来公开这些值，因此传输特征可能在所有情况下均不可用，也可能不可用。 因此，当 IOCTL 请求失败时，客户端驱动程序必须通过其他机制来确定信息。 

### <a name="query-for-the-current-transport-characterisctics"></a>查询当前传输 characterisctics

客户端驱动程序可以通过发送   [IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics) 请求来在特定时间查询传输特性。 收到请求后，USB 驱动程序堆栈会立即用有关 USB_TRANSPORT_CHARACTERISTICS 结构中当前传输特征的信息完成此过程。 假设信息不会在任何时间都指示更改，驱动程序可以使用该请求来决定算法或启动流。 

### <a name="receive-changes-in-trasport-characteristics"></a>接收 trasport 特征中的更改
对于 MA USB，基础传输可以是有线无线的。 随着时间的推移，这些媒体的传输特性可能会有很大差异。 客户端驱动程序可以获得有关正在进行的更改的通知。

1.    发送 [IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change) 请求以注册通知。 如果注册成功，则客户端驱动程序将收到传输特征的句柄和初始值。

2.  使用在步骤1中获取的注册句柄发送 [IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change) 请求。 USB 驱动程序堆栈会使请求处于挂起状态。 传输特征发生更改时，将以传输特征的新值完成挂起的请求。

3.  完成客户端并不想获取进一步的通知后，它应确保在堆栈中没有挂起的 IOCTLs，然后通过子代码 [IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)发送 IOCTL，并传入注册句柄。 如果客户端用挂起的更改请求取消注册，则在完成注销 IOCTL 之前，USB Stack 将完成这些请求。

### <a name="query-for-device-characteristics"></a>查询设备特征

若要 determione 有关 USB 设备的常规特征，例如任何请求的最大发送和接收延迟，客户端驱动程序可以发送  [IOCTL_USB_GET_DEVICE_CHARACTERISTICS](/windows-hardware/drivers/ddi/usbioctl/ns-usbioctl-_usb_device_characteristics) 请求。

## <a name="setting-priority-for-a-bulk-endpoint"></a>为大容量终结点设置优先级

在某些情况下，某些客户端驱动程序使用大容量终结点来容纳不同类型的数据，这些数据不符合大容量传输的优先级类。 例如，USB 显示器驱动程序可以使用大容量终结点来携带显示帧和光标更新。 用于 MIDI 的 USB 音频驱动程序可以使用大容量终结点来携带音频/语音数据。
对于使用此类客户端驱动程序的带外 USB 的用户体验，驱动程序必须根据数据类型确定大容量传输的优先级。 例如，带有鼠标光标更新或音频/语音数据的批量终结点应标记为最高优先级，而携带显示/视频或存储数据的批量终结点应标记为 "中优先级"。

客户端驱动程序可通过定义设备的 HW 注册表项的设备参数子项中特定批量终结点的 priorties 设置这些选项。  

注册表值的格式为名为 **EndpointPriorities**的多字符串。  多字符串中的每个字符串定义了特定终结点的优先级。  此字符串的格式如下所示： "，，，，， <CONFIG> <INTERFACE> <ALTSETTING> <TYPE> <ORDER> <PRIORITY> "

其中：

-    CONFIG –一个小数值，指示包含终结点的配置的 **bConfigurationValue** 值（在配置描述符中定义）。  值0无效。  可以指定通配符值 "*" 来指示它适用于所有配置。

-    接口-一个小数值，指示在包含终结点的配置（如接口描述符中定义）中接口的 **bInterfaceNumber** 。  可以指定通配符值 "*" 来指示它适用于所有接口。  如果注册表设置应用于复合 USB 函数而不是整个 USB 设备，则接口值将指示。

-    ALTSETTING-指示接口的替代设置的 bAlternateSetting 值的十进制值。  通配符值 "*" 可用于指示它适用于接口内的所有备用设置。

-    类型-指示指定的终结点的类型和方向。  有效字符串为 **BULK_IN**、 **BULK_OUT**、 **INTERRUPT_IN**、 **INTERRUPT_OUT**、 **ISOCHRONOUS_IN**、 **ISOCHRONOUS_OUT**和 **控件**。  

-    位置-一个从零开始的小数值，指示应用优先级的接口中的哪个终结点。  例如，如果接口有三个 BULK_OUT 终结点，则第一个终结点由位置值0指定，第二个终结点为1，依此类推。  对于复合 USB 设备上的函数，接口编号与分配给复合函数)  (的接口相关，而不是父 USB 设备。

例如，

```cpp

REG_MULTI_SZ:"EndpointPriorities" = 
“"1,0,*,BULK_IN,0,VIDEO",   // BULK IN endpoint in interface 0, configuration 1, all alternate settings has VIDEO priority. 
"1,1,*,BULK_OUT,0,VOICE",  // First BULK OUT endpoint in interface 1, configuration 1, all alternate settings has VOICE priority. 
"2,1,0,BULK_OUT,1,INTERACTIVE"” // BULK OUT endpoint in configuration 2, interface 1, alt setting 1 has INTERACTIVE priority.
```
## <a name="see-also"></a>另请参阅
[WdfUsbTargetDeviceCreateUrb](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)

[USBD_UrbAllocate](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate) 
[IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics)

[IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change)

[IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change)

[IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)