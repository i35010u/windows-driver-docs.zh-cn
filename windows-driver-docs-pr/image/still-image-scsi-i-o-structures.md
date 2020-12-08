---
title: 静态图像 SCSI I/O 结构
description: 静态图像 SCSI I/O 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07223d5551d64ac702d1000d9f0dd5aa072489f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836427"
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
<th>描述</th>
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

 

这些结构在 *scsiscan* 中定义。

