---
title: PCI Express 设备的容器 Id
description: PCI Express 设备的容器 Id
ms.assetid: ff86def3-a278-4f7b-a394-42f608f8993d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e234d54d0a83bd7e90ac1742fe851e09687421fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525713"
---
# <a name="container-ids-for-pci-express-devices"></a>PCI Express 设备的容器 Id


PCI Express (PCIe) 总线不能表达的容器 id。 PCI 总线驱动程序返回时确定 PCIe 设备分组的设备容器的可移动功能依赖于 Windows 操作系统。

PCI 总线驱动程序确定 PCIe 设备是通过阅读以下 PCIe 寄存器位可移动。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCIe 注册</th>
<th align="left">字节偏移量</th>
<th align="left">位位置</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PCI Express 功能</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>8-slot 实现</p></td>
<td align="left"><p>设置为 1 时，此位值指示与此端口相关联的 PCIe 链接已连接到物理槽，而不是连接到一个集成组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>槽功能</p></td>
<td align="left"><p>0x14</p></td>
<td align="left"><p>6-热插拔支持</p></td>
<td align="left"><p>设置为 1 时，此位值指示此槽可以支持热插拔操作。</p></td>
</tr>
</tbody>
</table>

 

PCI 总线驱动程序将标记 PCIe 设备为可移动，如果满足两个以下条件：

-   槽实现位设置为 1。

-   热即插即用支持的位设置为 1:

用于设置这些机制注册位按 PCIe 芯片集版本和制造商而异。 例如，某些芯片集让程序这些位的固件，而其他芯片集需要物理插针，以将 strapped 电压费用连接 (Vcc) 或全新 (GND)。

请注意，如果设备在 ACPI 名称空间中实现 _EJ0 方法，ACPI 驱动程序会将标记为可移动设备。 而不考虑槽实现或热即插即用支持 bits 的设置发生这种情况。 有关详细信息，请参阅[热插拔 PCI 和 Windows](https://go.microsoft.com/fwlink/p/?linkid=26278)白皮书。

PCIe 接口的详细信息，请参阅[PCIe 基本](https://go.microsoft.com/fwlink/p/?linkid=69486)规范。

 

 





