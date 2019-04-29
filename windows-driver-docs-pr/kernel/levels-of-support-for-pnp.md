---
title: PnP 的支持级别
description: PnP 的支持级别
ms.assetid: 33e0b4c6-858c-4822-ba49-38eb87a5923d
keywords:
- 即插即用 WDK 内核、 设备支持
- 插 WDK 内核、 设备支持
- 完整的即插即用 WDK 内核
- 部分即插即用 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1cff716770493462329a32569282fadae54c570
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381374"
---
# <a name="levels-of-support-for-pnp"></a>PnP 的支持级别





即插即用设备支持的程度取决于设备硬件和设备驱动程序 （请参阅下表） 中的即插即用支持。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>即插即用驱动程序</th>
<th>非 PnP 驱动程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>即插即用设备</strong></p></td>
<td><p>完整即插即用</p></td>
<td><p>不即插即用</p></td>
</tr>
<tr class="even">
<td><p><strong>非 PnP 设备</strong></p></td>
<td><p>可能的部分即插即用</p></td>
<td><p>不即插即用</p></td>
</tr>
</tbody>
</table>

 

支持即插即用的任何设备中的驱动程序应具有即插即用支持。

如果它由即插即用驱动程序，非 PnP 设备可具有一些即插即用功能。 例如，ISA 声卡或 EISA 网络卡可以手动安装和即插即用驱动程序然后可以将卡即插即用设备等。

如果驱动程序不支持即插即用，其设备的行为为非 PnP 设备而不考虑任何硬件即插即用支持。 非 PnP 驱动程序可以限制整个系统的即插即用和电源管理功能。

*旧式驱动程序*(即，在支持的操作系统之前编写的驱动程序 PnP) 继续像以前，如果没有任何即插即用功能。 新的驱动程序应包括即插即用支持。

 

 




