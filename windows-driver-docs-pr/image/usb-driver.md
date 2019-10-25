---
title: USB 驱动程序
description: USB 驱动程序
ms.assetid: c20bd393-98d0-498e-a3e8-bbd1958ed774
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8d4421e0dbaace2a3f3e101a85b0540d974185b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840733"
---
# <a name="usb-driver"></a>USB 驱动程序





USB 总线的内核模式静止映像驱动程序支持单个控制终结点和多个中断、大容量传入和批量输出终结点。 可以使用 i/o 控制代码和[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)访问控件和中断端点。 使用**ReadFile**和**WriteFile**可以访问大容量终结点。

在调用[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)、 **ReadFile**或**WriteFile**之前，必须调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) （Microsoft Windows SDK 文档中所述）来获取设备句柄。 对于不支持多个终结点类型的设备（控制、中断、大容量、批量输出），对**CreateFile**的单一调用会打开到每个终结点的传输管道。

对于支持多个中断或大容量终结点的设备，对[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)的单个调用会打开传输管道到每个类型的最高编号终结点。 如果要使用不同的终结点，则必须执行以下操作：

1.  调用[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)，指定 IOCTL 的 i/o 控制代码[ **\_获取\_管道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_pipe_configuration)，以确定端口的终结点索引号（即，返回到返回的[**USBSCAN\_管道的索引\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_pipe_information)结构数组）。 请注意，这些索引号*不*是*通用串行总线规范*中所述的终结点号。

2.  调用 CreateFile 时，将反斜杠和终结点的索引号追加到[**IStiDeviceControl：： GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)返回的端口名称。

例如，假设某个设备（端口名称为 "usbscan0"）具有两个类型（中断、大容量、大容量）的两个终结点，索引号如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>索引</th>
<th>在任务栏的搜索框中键入</th>
<th>终结点#</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>妨碍</p></td>
<td><p>0x01</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>批量</p></td>
<td><p>0x82</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>批量</p></td>
<td><p>0x83</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>批量输出</p></td>
<td><p>0x04</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>批量输出</p></td>
<td><p>0x05</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>妨碍</p></td>
<td><p>0x06</p></td>
</tr>
</tbody>
</table>

 

如果调用端口名称为 "usbscan0" 的[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) ，则该函数将向索引值为2、4和5的终结点以及控制终结点打开传输管道。

如果调用端口名称为 "usbscan0\\1" 的[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) ，则该函数会打开将管道传输到索引值为1、4和5的终结点，以及控制终结点。

对于此设备，如果要使用中断终结点0（在终结点1中大容量）和批量输出终结点3，请调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)三次，并指定 "usbscan0\\0"、"usbscan0\\1" 和 "usbscan0\\3" 的端口名称。 这将创建三个设备句柄。 每次调用[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)、 **ReadFile**或**WriteFile**时，都应指定与所需管道关联的设备句柄。

由于只支持一个控制终结点，因此，指定使用控制管道的任何 i/o 控制代码都会导致驱动程序使用正确的终结点，而不管将哪个终结点（如果有）指定到[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)。

有关所有 i/o 控制代码的说明，请参阅[USB 静止图像 I/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)。

内核模式 USB 驱动程序未实现包或消息协议。 读取操作不需要任何特定的数据包对齐方式，但如果读取请求与最大数据包大小边界对齐，则可以获得更好的性能。 可以使用 IOCTL 获取最大数据包大小， [ **\_获取\_通道\_对齐\_RQST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_channel_align_rqst) i/o 控制代码。

 

 




