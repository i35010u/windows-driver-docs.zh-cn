---
title: 仍映像 USB I/O 控制代码
description: 仍映像 USB I/O 控制代码
ms.assetid: 66a06a25-2fcb-4b14-85e2-485d2d4ac9d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4931d8aba4c280913e55b1a124743c1acc1805a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527173"
---
# <a name="still-image-usb-io-control-codes"></a>仍映像 USB I/O 控制代码





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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542843" data-raw-source="[&lt;strong&gt;IOCTL_CANCEL_IO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542843)"><strong>IOCTL_CANCEL_IO</strong></a></p></td>
<td><p>取消指定的 USB 传输管道上的活动。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542849" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542849)"><strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a></p></td>
<td><p>返回 USB 设备&#39;s 最大数据包大小为读取、 写入和中断传输管道。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542856" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542856)"><strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>返回供应商和设备标识符。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542859" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542859)"><strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>返回每个传输管道支持的设备的说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542864" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542864)"><strong>IOCTL_GET_USB_DESCRIPTOR</strong></a></p></td>
<td><p>返回指定的 USB 描述符。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542866" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542866)"><strong>IOCTL_GET_VERSION</strong></a></p></td>
<td><p>返回该驱动程序的版本号。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542869" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542869)"><strong>IOCTL_READ_REGISTERS</strong></a></p></td>
<td><p>从 USB 设备寄存器中，使用控制管道读取。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542872" data-raw-source="[&lt;strong&gt;IOCTL_RESET_PIPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542872)"><strong>IOCTL_RESET_PIPE</strong></a></p></td>
<td><p>重置指定的 USB 传输管道。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542900" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542900)"><strong>IOCTL_SEND_USB_REQUEST</strong></a></p></td>
<td><p>将供应商定义的请求发送到 USB 设备时，使用控制管道，可以选择发送或接收额外的数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542908" data-raw-source="[&lt;strong&gt;IOCTL_SET_TIMEOUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542908)"><strong>IOCTL_SET_TIMEOUT</strong></a></p></td>
<td><p>USB 大容量 IN、 OUT，大容量或中断管道访问设置的超时值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542917" data-raw-source="[&lt;strong&gt;IOCTL_WAIT_ON_DEVICE_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542917)"><strong>IOCTL_WAIT_ON_DEVICE_EVENT</strong></a></p></td>
<td><p>返回有关 USB 中断管道上发生的事件的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542920" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542920)"><strong>IOCTL_WRITE_REGISTERS</strong></a></p></td>
<td><p>将写入到 USB 设备寄存器中，使用控制管道。</p></td>
</tr>
</tbody>
</table>

 

这些代码中定义*usbscan.h*。 详细了解这些 I/O 控制代码，请参阅：

[USB 静止图像 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff548569)

 

 




