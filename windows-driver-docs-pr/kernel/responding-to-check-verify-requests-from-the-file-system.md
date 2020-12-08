---
title: 响应来自文件系统的 Check-Verify 请求
description: 响应来自文件系统的 Check-Verify 请求
keywords:
- 可移动媒体 WDK 内核，检查-验证请求
- 检查-验证请求 WDK 可移动介质
- 媒体更改请求 WDK 可移动介质
- 正在检查可移动媒体更改
- 验证可移动媒体更改
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2f4cbfba9cca0a1f7bcc7a773a1c63d15c7fd41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820627"
---
# <a name="responding-to-check-verify-requests-from-the-file-system"></a>响应来自文件系统的 Check-Verify 请求





为此，文件系统可以将 IRP 发送到设备驱动程序的调度入口点，以便在 i/o 堆栈位置设置为 **DeviceIoControl. IoControlCode** ，并将其设置为以下内容： [**\_ \_ \_**](./irp-mj-device-control.md)

<a href="" id="ioctl-xxx-check-verify"></a>IOCTL \_ *XXX* \_ 检查 \_ 验证  
其中 *XXX* 是设备的类型，例如磁盘、磁带或 CDROM。

类型磁盘包括 unpartitionable (软盘) 和分区可移动介质设备。

如果基础设备驱动程序确定媒体尚未更改，则驱动程序应完成 IRP，并返回 **IoStatus** 块，并返回以下值：

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

 

此外，如果设备类型为 DISK 或 CDROM，并且调用方指定了输出缓冲区，则驱动程序将在 **&gt; temBuffer 的** 中返回AssociatedIrp.Sys缓冲区中的媒体更改计数，并将 **irp- &gt; IOSTATUS** 设置为 **sizeof** (ULONG) 。 通过返回此计数，该驱动程序为调用方提供一个机会来确定媒体是否已从其角度进行了更改。

如果基础设备驱动程序确定媒体已更改，则会根据卷是否已装入来执行不同的操作。 如果已装入卷 (在 \_ VPB) 中设置 VPB 装入标志，则驱动程序应执行以下操作：

1.  将 **DeviceObject** By or **标志** 中的 **标志** 设置为 DO \_ VERIFY \_ VOLUME。

2.  将 IRP 中的 **IoStatus** 块设置为以下内容：
    -   **状态** 设置为 " \_ 需要验证" \_
    -   **信息** 设置为零

3.  将 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 与输入 IRP 一起调用。

如果未装入卷，则驱动程序不得设置 " \_ 验证 \_ 卷" 位。 驱动程序应将 **IoStatus** 设置为状态 \_ IO \_ 设备 \_ 错误，将 **IoStatus** 设置为零，并通过 IRP 调用 **IoCompleteRequest** 。

 

