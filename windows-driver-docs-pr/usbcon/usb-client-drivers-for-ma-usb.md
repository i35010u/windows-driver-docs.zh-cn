---
Description: USB 发送 MA USB 数据包的设备驱动程序。
title: 不区分媒体的 (MA-USB) 协议的客户端驱动程序
ms.date: 09/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9bb01d052ea99f135e23811611bb71cc04385b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368750"
---
# <a name="usb-client-drivers-for-media-agnostic-ma-usb"></a>不区分媒体的 (MA-USB) 协议的客户端驱动程序

在 Windows 10 版本 1709，USB 驱动程序堆栈可以通过非 USB 物理媒体，如 Wi-fi 发送 USB 数据包，通过使用媒体不可知的 USB (MA USB) 协议。 现有 USB 客户端驱动程序所需的更改是最小的方式设计的新功能。 更改该设置包含有关传输的其他信息：

-   对于设备与同步/流式处理终结点，客户端驱动程序需要知道与编程的传输相关联的延迟，以便该驱动程序可以确保设备在时间上获取同步的数据包传输完成。

-   客户端驱动程序可以使用该 informationf 优化其更高的层选择的协议。 例如，显示驱动程序可以使用的延迟和带宽的信息来选择最佳的编解码器和缓冲方案。 因为这些特征可能会动态更改，该驱动程序必须确定所做的更改。

## <a name="getting-the-delays-for-isochronous-transfers"></a>获取对同步传输的延迟

对于同步终结点，客户端驱动程序需要知道的编程的最大延迟和最大完成延迟。 该请求必须针对特定的管道，因为该延迟可能是不同的同一设备上的不同终结点，如 MA USB 规范提供了主机来计算这些值的机制。 

若要生成该驱动程序必须使用该请求 **_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS** URB。

> [!NOTE]
> 在此版本中，此功能目前仅 KMDF 和基于 WDM 驱动程序。 

下面是用于构建此 URB 一些最佳实践：


-    客户端 dirver 必须通过调用分配此 URB [WdfUsbTargetDeviceCreateUrb](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)或[USBD_UrbAllocate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urballocate)。 
- 可以在发送 URB < = 调度级别。
- 如果 URB 到等非同步终结点为目标，USB 驱动程序堆栈使请求失败。
- 客户端驱动程序必须假定此 URB 受第三方 USB 堆栈。 所有 Microsoft 将会都支持该 = 提供收件箱 USB 客户端驱动程序。

对于连续同步在流中，客户端驱动程序通常将发出多个未完成的读取的请求。 该驱动程序可以使用的往返时间来计算等时，需要在基于未完成的读取请求数的读取请求的数据包数。

例如，如果两个未完成的请求数，在 URB 同步数据包数至少应为 （总往返时间） / （服务间隔长度） 其中总往返行程时间 = MaximumSendPathDelayInMilliSeconds +MaximumCompletionPathDelayInMilliSeconds

如果发送延迟 = 10 毫秒、 完成延迟 = 15msec，则总往返 = 25msec。
如果服务间隔长度 = 5 毫秒数等时 URBs = 2 连续流式处理的每个同步 URBs 等时数据包数量应为至少 = 25 / 5 = 5 个数据包。

## <a name="getting-the-host-controller-transport-characteristics"></a>获取主机控制器传输特征
客户端驱动程序可以通过发送这些 Ioctl 请求来检索的传输特征：

-    [IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics)
-    [IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change)
-    [IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change) 
-    [IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)

传输特征可能或不可能是在所有情况下可用的因为 USB 驱动程序堆栈是依赖于基础传输公开这些值。 因此，客户端驱动程序必须确定哪些信息通过其他机制 IOCTL 请求失败时。 

### <a name="query-for-the-current-transport-characterisctics"></a>查询当前传输 characterisctics

客户端驱动程序可以查询的传输特征在特定时间发送[IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics)请求。 收到请求后，USB 驱动程序堆栈完成后，它立即 USB_TRANSPORT_CHARACTERISTICS 结构中的当前传输特征有关的信息。 考虑到信息并不表示可以确定该算法或启动流驱动程序使用在任何时候，此请求的更改。 

### <a name="receive-changes-in-trasport-characteristics"></a>接收在 trasport 特征中的更改
MA USB、 基础传输可能有线、 无线。 随着时间的推移有这些介质的传输特征显著变化。 客户端驱动程序可以获取有关正在发生的更改的通知。

1.    发送[IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change)请求以注册通知。 如果注册成功，客户端驱动程序将接收一个句柄和传输特征的初始值。

2.  发送[IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change)请求与在步骤 1 中的注册句柄。 USB 驱动程序堆栈保留挂起的请求。 只要传输特征更改，挂起的请求已完成并且传输特征的新值。

3.  完成客户端并不希望获取进一步的通知，它应确保那里后是挂起的堆栈中没有 Ioctl，然后发送子代码 IOCTL [IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)，并传入注册句柄。 如果客户端注销具有挂起的更改请求，USB 堆栈将完成其完成注销 IOCTL 之前。

### <a name="query-for-device-characteristics"></a>设备特征的查询

到 determione 有关 USB 设备，例如最大的常规特征发送和接收的任何请求延迟客户端驱动程序可以发送[IOCTL_USB_GET_DEVICE_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ns-usbioctl-_usb_device_characteristics)请求。

## <a name="setting-priority-for-a-bulk-endpoint"></a>设置为大容量终结点的优先级

可能情况下，某些客户端驱动程序将用于携带不同类型的大容量传输的优先级类无法容纳的数据大容量终结点时。 例如，USB 显示器驱动程序可以使用大容量终结点执行显示帧和游标更新。 MIDI 的 USB 音频驱动程序可以使用大容量终结点执行音频/语音数据。
为用户良好的体验通过 MA USB 此类客户端驱动程序，该驱动程序必须确定优先级基于的数据类型的大容量传输。 例如，大容量终结点，带有鼠标光标更新或音频/语音数据应标记最高优先级而携带显示/视频或存储数据的大容量终结点应标记为中等优先级。

客户端驱动程序可以通过在设备的硬件注册表项的设备参数子项中定义的特定批量终结点 priorties 设置选项。  

注册表值的格式是名为 multistring **EndpointPriorities**。  多字符串内的每个字符串定义为特定终结点的优先级。  字符串的格式如下所示:"<CONFIG>，<INTERFACE>，<ALTSETTING>，<TYPE>，<ORDER>，<PRIORITY>"

其中：

-    配置 – 一个十进制值，该值指示**bConfigurationValue**包含的终结点，配置描述符中定义的配置值。  值 0 不是有效的。  通配符值为"*"可指定以指示它适用于所有配置。

-    接口的一个十进制值，该值指示**bInterfaceNumber**包含接口描述符中定义的终结点，在配置中的接口。  通配符值为"*"可指定以指示它适用于所有接口。  在注册表设置为一个复合 USB 函数而不是整个的 USB 设备应用的位置的情况下，将指示界面值。

-    ALTSETTING 的十进制值，该值指示该接口的 bAlternateSetting 值的替代设置。  通配符值为"*"可用于指示它适用于在界面中的所有替代设置。

-    类型-指示的类型和指定的终结点的方向。  有效字符串为**BULK_IN**， **BULK_OUT**， **INTERRUPT_IN**， **INTERRUPT_OUT**， **ISOCHRONOUS_IN**， **ISOCHRONOUS_OUT**，并**控制**。  

-    位置的从零开始的十进制值，该值指示在界面中的哪个终结点应用到的优先级。  例如，如果接口有三个 BULK_OUT 终结点由位置值为 0，1，等的第二个终结点指定第一个终结点。  对于复合的 USB 设备上的函数接口号是相对于接口分配给复合函数，而非父 USB 设备。

例如，

```cpp

REG_MULTI_SZ:"EndpointPriorities" = 
“"1,0,*,BULK_IN,0,VIDEO",   // BULK IN endpoint in interface 0, configuration 1, all alternate settings has VIDEO priority. 
"1,1,*,BULK_OUT,0,VOICE",  // First BULK OUT endpoint in interface 1, configuration 1, all alternate settings has VOICE priority. 
"2,1,0,BULK_OUT,1,INTERACTIVE"” // BULK OUT endpoint in configuration 2, interface 1, alt setting 1 has INTERACTIVE priority.
```
## <a name="see-also"></a>请参阅
[WdfUsbTargetDeviceCreateUrb](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)

[USBD_UrbAllocate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urballocate)
[IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics)

[IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change)

[IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change)

[IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)
