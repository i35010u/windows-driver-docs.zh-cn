---
title: PnP 的支持级别
description: PnP 的支持级别
keywords:
- PnP WDK 内核，设备支持
- 即插即用 WDK 内核，设备支持
- 完全 PnP WDK 内核
- 部分 PnP WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c47c5e666d18fb936a982f1465545ead6fbc7c80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801669"
---
# <a name="levels-of-support-for-pnp"></a>PnP 的支持级别





设备支持 PnP 的程度取决于设备硬件和设备驱动程序中的 PnP 支持 (参阅下表) 。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>PnP 驱动程序</th>
<th>非 PnP 驱动程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PnP 设备</strong></p></td>
<td><p>完全 PnP</p></td>
<td><p>无 PnP</p></td>
</tr>
<tr class="even">
<td><p><strong>非 PnP 设备</strong></p></td>
<td><p>可能的部分 PnP</p></td>
<td><p>无 PnP</p></td>
</tr>
</tbody>
</table>

 

支持 PnP 的任何设备应在其驱动程序中提供 PnP 支持。

如果非 PnP 设备由 PnP 驱动程序驱动，则它可以具有一些 PnP 功能。 例如，可以手动安装 ISA 声卡或 EISA 网卡，然后 PnP 驱动程序可以将该卡视为 PnP 设备。

如果驱动程序不支持 PnP，则其设备将表现为非 PnP 设备，而不考虑任何硬件 PnP 支持。 非 PnP 驱动程序可以限制整个系统的 PnP 和电源管理功能。

*旧的驱动程序* (即，在操作系统支持的 PnP 之前编写的驱动程序) 继续像以前一样工作，无需任何 PnP 功能。 新驱动程序应包括 PnP 支持。

 

 




