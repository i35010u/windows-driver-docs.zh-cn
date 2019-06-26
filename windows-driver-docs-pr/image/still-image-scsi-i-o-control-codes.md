---
title: 静态图像 SCSI I/O 控制代码
description: 静态图像 SCSI I/O 控制代码
ms.assetid: 8db15071-61ac-4bb3-9193-da854a15f376
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fcdd2b9af03e348b66404cc8cf7928301a4e7e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371921"
---
# <a name="still-image-scsi-io-control-codes"></a>静态图像 SCSI I/O 控制代码





下表列出并描述所有识别的内核模式下仍映像驱动程序对于 SCSI 总线的 I/O 控制代码。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd)"><strong>IOCTL_SCSISCAN_CMD</strong></a></p></td>
<td><p>创建自定义的 SCSI 控制描述符块并将其发送到内核模式下仍映像驱动程序对于 SCSI 总线。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info)"><strong>IOCTL_SCSISCAN_GET_INFO</strong></a></p></td>
<td><p>返回设备的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_lockdevice" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_LOCKDEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_lockdevice)"><strong>IOCTL_SCSISCAN_LOCKDEVICE</strong></a></p></td>
<td><p>保留供 microsoft 使用。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_set_timeout" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_SET_TIMEOUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_set_timeout)"><strong>IOCTL_SCSISCAN_SET_TIMEOUT</strong></a></p></td>
<td><p>修改由内核模式下仍映像驱动程序用于 SCSI 总线访问设备时的超时值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_unlockdevice" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_UNLOCKDEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_unlockdevice)"><strong>IOCTL_SCSISCAN_UNLOCKDEVICE</strong></a></p></td>
<td><p>保留供 microsoft 使用。</p></td>
</tr>
</tbody>
</table>

 

这些代码中定义*scsiscan.h*。

 

 




