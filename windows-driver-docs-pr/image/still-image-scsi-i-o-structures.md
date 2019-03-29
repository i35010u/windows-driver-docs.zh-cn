---
title: 静态图像 SCSI I/O 结构
description: 静态图像 SCSI I/O 结构
ms.assetid: 2cf17295-e3af-4109-bfdd-118aecf80bbe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b29e25a911176defefcfde0d864fd332d91cfac8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567118"
---
# <a name="still-image-scsi-io-structures"></a>静态图像 SCSI I/O 结构





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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547972" data-raw-source="[&lt;strong&gt;SCSISCAN_CMD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547972)"><strong>SCSISCAN_CMD</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542877" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542877)"> <strong>IOCTL_SCSISCAN_CMD</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547981" data-raw-source="[&lt;strong&gt;SCSISCAN_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547981)"><strong>SCSISCAN_INFO</strong></a></p></td>
<td><p>使用作为参数<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>，当指定的 I/O 控制代码时， <a href="https://msdn.microsoft.com/library/windows/hardware/ff542879" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542879)"> <strong>IOCTL_SCSISCAN_GET_INFO</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

这些结构中定义*scsiscan.h*。

 

 




