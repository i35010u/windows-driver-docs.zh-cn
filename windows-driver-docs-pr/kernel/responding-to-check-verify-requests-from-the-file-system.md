---
title: 响应来自文件系统的 Check-Verify 请求
description: 响应来自文件系统的 Check-Verify 请求
ms.assetid: 227e65d6-d746-4b16-978d-4d42be9aeb2c
keywords:
- 可移动媒体 WDK 内核，检查-验证请求
- 检查-验证请求 WDK 可移动介质
- 媒体更改请求 WDK 可移动介质
- 正在检查可移动媒体更改
- 验证可移动媒体更改
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf2df0db0d517079ab1c5254dbda682522ec949
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838446"
---
# <a name="responding-to-check-verify-requests-from-the-file-system"></a>响应来自文件系统的 Check-Verify 请求





根据其判断，文件系统可以将 IRP 发送到设备驱动程序的调度入口点，以便[**irp\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求，并将 i/o 堆栈位置中的**IoControlCode**设置为之后

<a href="" id="ioctl-xxx-check-verify"></a>IOCTL\_*XXX*\_检查\_验证  
其中*XXX*是设备的类型，例如磁盘、磁带或 CDROM。

类型磁盘包括 unpartitionable （软盘）和分区可移动介质设备。

如果基础设备驱动程序确定媒体尚未更改，则驱动程序应完成 IRP，并返回**IoStatus**块，并返回以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>状态</strong></p></td>
<td><p>设置为 STATUS_SUCCESS</p></td>
</tr>
<tr class="even">
<td><p><strong>信息</strong></p></td>
<td><p>设置为零</p></td>
</tr>
</tbody>
</table>

 

此外，如果设备类型为 DISK 或 CDROM，并且调用方指定了输出缓冲区，则驱动程序将在**AssociatedIrp SystemBuffer**中返回&gt;缓冲区中的媒体更改计数，并将**Irp-&gt;IoStatus**设置为**sizeof**（ULONG）。 通过返回此计数，该驱动程序为调用方提供一个机会来确定媒体是否已从其角度进行了更改。

如果基础设备驱动程序确定媒体已更改，则会根据卷是否已装入来执行不同的操作。 如果已装入卷（在 VPB 中设置 VPB\_装载标志），驱动程序应执行以下操作：

1.  将**DeviceObject** By or**标志**中的**标志**设置为 DO\_验证\_卷。

2.  将 IRP 中的**IoStatus**块设置为以下内容：
    -   **状态**设置为状态\_验证是否需要\_
    -   **信息**设置为零

3.  将[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)与输入 IRP 一起调用。

如果未装入卷，则驱动程序不得设置 DO\_验证\_卷位。 驱动程序应将**IoStatus**设置为状态\_IO\_设备\_错误，将**IoStatus**设置为零，并通过 IRP 调用**IoCompleteRequest** 。

 

 




