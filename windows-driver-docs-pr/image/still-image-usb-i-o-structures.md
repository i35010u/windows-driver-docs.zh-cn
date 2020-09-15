---
title: 静态图像 USB I/O 结构
description: 静态图像 USB I/O 结构
ms.assetid: d70c5c11-c8f2-4196-a7f5-d97ceef10ca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cf5a81a97643d66c251f7dd149d8dc823594476
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107178"
---
# <a name="still-image-usb-io-structures"></a>静态图像 USB I/O 结构





下表列出并描述了与 i/o 控制代码（SCSI 总线的内核模式静止映像驱动程序识别）关联的所有结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>结构</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_channel_info" data-raw-source="[&lt;strong&gt;CHANNEL_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_channel_info)"><strong>CHANNEL_INFO</strong></a></p></td>
<td><p>当指定<a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_channel_align_rqst" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_channel_align_rqst)"><strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a>的 i/o 控制代码时，用作<a href="/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_device_descriptor" data-raw-source="[&lt;strong&gt;DEVICE_DESCRIPTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_device_descriptor)"><strong>DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>当指定<a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_device_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_device_descriptor)"><strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a>的 i/o 控制代码时，用作<a href="/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_drv_version" data-raw-source="[&lt;strong&gt;DRV_VERSION&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_drv_version)"><strong>DRV_VERSION</strong></a></p></td>
<td><p>当指定<a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_version" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_version)"><strong>IOCTL_GET_VERSION</strong></a>的 i/o 控制代码时，用作<a href="/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_io_block" data-raw-source="[&lt;strong&gt;IO_BLOCK&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_io_block)"><strong>IO_BLOCK</strong></a></p></td>
<td><p>当指定的 i/o 控制代码<a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_read_registers" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_read_registers)"><strong>IOCTL_READ_REGISTERS</strong></a>或<a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_write_registers" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_write_registers)"><strong>IOCTL_WRITE_REGISTERS</strong></a>时，用作<a href="/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_io_block_ex" data-raw-source="[&lt;strong&gt;IO_BLOCK_EX&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_io_block_ex)"><strong>IO_BLOCK_EX</strong></a></p></td>
<td><p>当指定<a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_send_usb_request" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_send_usb_request)"><strong>IOCTL_SEND_USB_REQUEST</strong></a>的 i/o 控制代码时，用作<a href="/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_get_descriptor" data-raw-source="[&lt;strong&gt;USBSCAN_GET_DESCRIPTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_get_descriptor)"><strong>USBSCAN_GET_DESCRIPTOR</strong></a></p></td>
<td><p>当指定<a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_usb_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_usb_descriptor)"><strong>IOCTL_GET_USB_DESCRIPTOR</strong></a>的 i/o 控制代码时，用作<a href="/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_pipe_configuration" data-raw-source="[&lt;strong&gt;USBSCAN_PIPE_CONFIGURATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_pipe_configuration)"><strong>USBSCAN_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>当指定<a href="/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_pipe_configuration" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_pipe_configuration)"><strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a>的 i/o 控制代码时，用作<a href="/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_pipe_information" data-raw-source="[&lt;strong&gt;USBSCAN_PIPE_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_pipe_information)"><strong>USBSCAN_PIPE_INFORMATION</strong></a></p></td>
<td><p>用于描述静止图像设备的 USB 传输管道。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_timeout" data-raw-source="[&lt;strong&gt;USBSCAN_TIMEOUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_timeout)"><strong>USBSCAN_TIMEOUT</strong></a></p></td>
<td><p>存储 USB 大容量和大容量操作和中断的超时值。</p></td>
</tr>
</tbody>
</table>

 

这些结构在 *usbscan*中定义。 有关这些结构的详细信息，请参阅：

[USB 静止图像结构](/windows-hardware/drivers/ddi/_image/index)

