---
title: 静态图像 SCSI I/O 控制代码
description: 静态图像 SCSI I/O 控制代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 524da59facd54d8fec9bee3eae1f557c2e44cfc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834533"
---
# <a name="still-image-scsi-io-control-codes"></a>静态图像 SCSI I/O 控制代码





下表列出并描述了用于 SCSI 总线的内核模式静止映像驱动程序识别的所有 i/o 控制代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>I/o 控制代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd)"><strong>IOCTL_SCSISCAN_CMD</strong></a></p></td>
<td><p>创建自定义 SCSI 控制描述符块，并将其发送到 SCSI 总线的内核模式静止映像驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info)"><strong>IOCTL_SCSISCAN_GET_INFO</strong></a></p></td>
<td><p>返回设备信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_lockdevice" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_LOCKDEVICE&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_lockdevice)"><strong>IOCTL_SCSISCAN_LOCKDEVICE</strong></a></p></td>
<td><p>保留以供 Microsoft 使用。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_set_timeout" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_SET_TIMEOUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_set_timeout)"><strong>IOCTL_SCSISCAN_SET_TIMEOUT</strong></a></p></td>
<td><p>修改在访问设备时，SCSI 总线的内核模式静止映像驱动程序所使用的超时值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_unlockdevice" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_UNLOCKDEVICE&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_unlockdevice)"><strong>IOCTL_SCSISCAN_UNLOCKDEVICE</strong></a></p></td>
<td><p>保留以供 Microsoft 使用。</p></td>
</tr>
</tbody>
</table>

 

这些代码在 *scsiscan* 中定义。

