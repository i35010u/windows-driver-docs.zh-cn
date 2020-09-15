---
title: 静态图像 USB I/O 控制代码
description: 静态图像 USB I/O 控制代码
ms.assetid: 66a06a25-2fcb-4b14-85e2-485d2d4ac9d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 006c66a07440060215e9d89a19e48970b6301191
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107180"
---
# <a name="still-image-usb-io-control-codes"></a>静态图像 USB I/O 控制代码





下表列出并描述了用于 USB 总线的内核模式静止映像驱动程序识别的所有 i/o 控制代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>I/o 控制代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_cancel_io" data-raw-source="[&lt;strong&gt;IOCTL_CANCEL_IO&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_cancel_io)"><strong>IOCTL_CANCEL_IO</strong></a></p></td>
<td><p>取消指定 USB 传输管道上的活动。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_channel_align_rqst" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_channel_align_rqst)"><strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a></p></td>
<td><p>为读取、写入和中断传输管道返回 USB 设备的最大数据包大小。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_device_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_device_descriptor)"><strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>返回供应商和设备标识符。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_pipe_configuration" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_pipe_configuration)"><strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>返回设备支持的每个传输管道的说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_usb_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_usb_descriptor)"><strong>IOCTL_GET_USB_DESCRIPTOR</strong></a></p></td>
<td><p>返回指定的 u 说明符。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_version" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_version)"><strong>IOCTL_GET_VERSION</strong></a></p></td>
<td><p>返回驱动程序的版本号。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_read_registers" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_read_registers)"><strong>IOCTL_READ_REGISTERS</strong></a></p></td>
<td><p>使用控制管道从 USB 设备寄存器进行读取。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_reset_pipe" data-raw-source="[&lt;strong&gt;IOCTL_RESET_PIPE&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_reset_pipe)"><strong>IOCTL_RESET_PIPE</strong></a></p></td>
<td><p>重置指定的 USB 传输管道。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_send_usb_request" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_send_usb_request)"><strong>IOCTL_SEND_USB_REQUEST</strong></a></p></td>
<td><p>使用控制管道将供应商定义的请求发送到 USB 设备，并根据需要发送或接收其他数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_set_timeout" data-raw-source="[&lt;strong&gt;IOCTL_SET_TIMEOUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_set_timeout)"><strong>IOCTL_SET_TIMEOUT</strong></a></p></td>
<td><p>设置 USB 批量输入、批量传出或中断管道访问的超时值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_wait_on_device_event" data-raw-source="[&lt;strong&gt;IOCTL_WAIT_ON_DEVICE_EVENT&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_wait_on_device_event)"><strong>IOCTL_WAIT_ON_DEVICE_EVENT</strong></a></p></td>
<td><p>返回有关 USB 中断管道上发生的事件的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_write_registers" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_write_registers)"><strong>IOCTL_WRITE_REGISTERS</strong></a></p></td>
<td><p>使用控制管道写入 USB 设备寄存器。</p></td>
</tr>
</tbody>
</table>

 

这些代码在 *usbscan*中定义。 有关这些 i/o 控制代码的详细信息，请参阅：

[USB 静止图像 i/o 控制代码](/windows-hardware/drivers/ddi/_image/index)

