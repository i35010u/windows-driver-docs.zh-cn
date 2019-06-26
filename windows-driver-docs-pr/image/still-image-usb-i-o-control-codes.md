---
title: 静态图像 USB I/O 控制代码
description: 静态图像 USB I/O 控制代码
ms.assetid: 66a06a25-2fcb-4b14-85e2-485d2d4ac9d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84750fd52d2c4add057c392694c2b61106e8631b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377700"
---
# <a name="still-image-usb-io-control-codes"></a>静态图像 USB I/O 控制代码





下表列出并描述所有内核模式下仍映像驱动程序对于 USB 总线识别 I/O 控制代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>I/O 控制代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_cancel_io" data-raw-source="[&lt;strong&gt;IOCTL_CANCEL_IO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_cancel_io)"><strong>IOCTL_CANCEL_IO</strong></a></p></td>
<td><p>取消指定的 USB 传输管道上的活动。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_channel_align_rqst" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_channel_align_rqst)"><strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a></p></td>
<td><p>返回读取、 写入和中断传输管道 USB 设备的最大数据包大小。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_device_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_device_descriptor)"><strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>返回供应商和设备标识符。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_pipe_configuration" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_pipe_configuration)"><strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>返回每个传输管道支持的设备的说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_usb_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_usb_descriptor)"><strong>IOCTL_GET_USB_DESCRIPTOR</strong></a></p></td>
<td><p>返回指定的 USB 描述符。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_version" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_version)"><strong>IOCTL_GET_VERSION</strong></a></p></td>
<td><p>返回该驱动程序的版本号。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_read_registers" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_read_registers)"><strong>IOCTL_READ_REGISTERS</strong></a></p></td>
<td><p>从 USB 设备寄存器中，使用控制管道读取。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_reset_pipe" data-raw-source="[&lt;strong&gt;IOCTL_RESET_PIPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_reset_pipe)"><strong>IOCTL_RESET_PIPE</strong></a></p></td>
<td><p>重置指定的 USB 传输管道。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_send_usb_request" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_send_usb_request)"><strong>IOCTL_SEND_USB_REQUEST</strong></a></p></td>
<td><p>将供应商定义的请求发送到 USB 设备时，使用控制管道，可以选择发送或接收额外的数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_set_timeout" data-raw-source="[&lt;strong&gt;IOCTL_SET_TIMEOUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_set_timeout)"><strong>IOCTL_SET_TIMEOUT</strong></a></p></td>
<td><p>USB 大容量 IN、 OUT，大容量或中断管道访问设置的超时值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_wait_on_device_event" data-raw-source="[&lt;strong&gt;IOCTL_WAIT_ON_DEVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_wait_on_device_event)"><strong>IOCTL_WAIT_ON_DEVICE_EVENT</strong></a></p></td>
<td><p>返回有关 USB 中断管道上发生的事件的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_write_registers" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_write_registers)"><strong>IOCTL_WRITE_REGISTERS</strong></a></p></td>
<td><p>将写入到 USB 设备寄存器中，使用控制管道。</p></td>
</tr>
</tbody>
</table>

 

这些代码中定义*usbscan.h*。 详细了解这些 I/O 控制代码，请参阅：

[USB 静止图像 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)

 

 




