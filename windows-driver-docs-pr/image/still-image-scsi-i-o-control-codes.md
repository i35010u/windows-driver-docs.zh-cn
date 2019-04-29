---
title: 静态图像 SCSI I/O 控制代码
description: 静态图像 SCSI I/O 控制代码
ms.assetid: 8db15071-61ac-4bb3-9193-da854a15f376
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f22e6c97679b2dd4334e1f5733c1b06cc4d2b2a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322285"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542877" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542877)"><strong>IOCTL_SCSISCAN_CMD</strong></a></p></td>
<td><p>创建自定义的 SCSI 控制描述符块并将其发送到内核模式下仍映像驱动程序对于 SCSI 总线。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542879" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542879)"><strong>IOCTL_SCSISCAN_GET_INFO</strong></a></p></td>
<td><p>返回设备的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542885" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_LOCKDEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542885)"><strong>IOCTL_SCSISCAN_LOCKDEVICE</strong></a></p></td>
<td><p>保留供 microsoft 使用。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542886" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_SET_TIMEOUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542886)"><strong>IOCTL_SCSISCAN_SET_TIMEOUT</strong></a></p></td>
<td><p>修改由内核模式下仍映像驱动程序用于 SCSI 总线访问设备时的超时值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542895" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_UNLOCKDEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542895)"><strong>IOCTL_SCSISCAN_UNLOCKDEVICE</strong></a></p></td>
<td><p>保留供 microsoft 使用。</p></td>
</tr>
</tbody>
</table>

 

这些代码中定义*scsiscan.h*。

 

 




