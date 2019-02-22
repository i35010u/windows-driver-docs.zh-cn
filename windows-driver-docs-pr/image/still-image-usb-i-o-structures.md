---
title: 静止图像 USB I/O 结构
description: 静止图像 USB I/O 结构
ms.assetid: d70c5c11-c8f2-4196-a7f5-d97ceef10ca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ffad556ddc7b2b202c7621b54d3ee7484749f26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555277"
---
# <a name="still-image-usb-io-structures"></a>静止图像 USB I/O 结构





下表列出并描述所有与内核模式下仍映像驱动程序识别的 SCSI 总线的 I/O 控制代码相关联的结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>结构</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539466" data-raw-source="[&lt;strong&gt;CHANNEL_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539466)"><strong>CHANNEL_INFO</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542849" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542849)"> <strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540576" data-raw-source="[&lt;strong&gt;DEVICE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540576)"><strong>DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542856" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542856)"> <strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541204" data-raw-source="[&lt;strong&gt;DRV_VERSION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541204)"><strong>DRV_VERSION</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542866" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542866)"> <strong>IOCTL_GET_VERSION</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542924" data-raw-source="[&lt;strong&gt;IO_BLOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542924)"><strong>IO_BLOCK</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542869" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542869)"> <strong>IOCTL_READ_REGISTERS</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff542920" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542920)"> <strong>IOCTL_WRITE_REGISTERS</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542928" data-raw-source="[&lt;strong&gt;IO_BLOCK_EX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542928)"><strong>IO_BLOCK_EX</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542900" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542900)"> <strong>IOCTL_SEND_USB_REQUEST</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548534" data-raw-source="[&lt;strong&gt;USBSCAN_GET_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548534)"><strong>USBSCAN_GET_DESCRIPTOR</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542864" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542864)"> <strong>IOCTL_GET_USB_DESCRIPTOR</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548541" data-raw-source="[&lt;strong&gt;USBSCAN_PIPE_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548541)"><strong>USBSCAN_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542859" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542859)"> <strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548547" data-raw-source="[&lt;strong&gt;USBSCAN_PIPE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548547)"><strong>USBSCAN_PIPE_INFORMATION</strong></a></p></td>
<td><p>用于描述静态图像设备的 USB 传输管道。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548554" data-raw-source="[&lt;strong&gt;USBSCAN_TIMEOUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548554)"><strong>USBSCAN_TIMEOUT</strong></a></p></td>
<td><p>存储在 USB 大容量和大容量操作的超时值并中断。</p></td>
</tr>
</tbody>
</table>

 

这些结构中定义*usbscan.h*。 这些结构，请参阅有关的详细信息：

[USB 静止图像结构](https://msdn.microsoft.com/library/windows/hardware/ff548574)

 

 




