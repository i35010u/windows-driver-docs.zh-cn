---
title: 静态图像 SCSI I/O 结构
description: 静态图像 SCSI I/O 结构
ms.assetid: 2cf17295-e3af-4109-bfdd-118aecf80bbe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee65f387e5c2b8db2a4158d0b452c2d5dd9c1451
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716212"
---
# <a name="still-image-scsi-io-structures"></a>静态图像 SCSI I/O 结构





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
<td><p><a href="/windows-hardware/drivers/ddi/scsiscan/ns-scsiscan-_scsiscan_cmd" data-raw-source="[&lt;strong&gt;SCSISCAN_CMD&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ns-scsiscan-_scsiscan_cmd)"><strong>SCSISCAN_CMD</strong></a></p></td>
<td><p>当指定<a href="/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd)"><strong>IOCTL_SCSISCAN_CMD</strong></a>的 i/o 控制代码时，用作<a href="/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/scsiscan/ns-scsiscan-_scsiscan_info" data-raw-source="[&lt;strong&gt;SCSISCAN_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ns-scsiscan-_scsiscan_info)"><strong>SCSISCAN_INFO</strong></a></p></td>
<td><p>当指定<a href="/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info)"><strong>IOCTL_SCSISCAN_GET_INFO</strong></a>的 i/o 控制代码时，用作<a href="/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>的参数。</p></td>
</tr>
</tbody>
</table>

 

这些结构在 *scsiscan*中定义。

