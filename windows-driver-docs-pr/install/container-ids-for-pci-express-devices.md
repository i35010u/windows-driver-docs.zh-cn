---
title: PCI Express 设备的容器 ID
description: PCI Express 设备的容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 063ce5f2a3213cf22f53f0a78eb93c114bed29d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827849"
---
# <a name="container-ids-for-pci-express-devices"></a>PCI Express 设备的容器 ID


PCI Express (PCIe) 总线无法表示容器 ID。 Windows 操作系统依赖于 PCI bus 驱动程序在确定 PCIe 设备的设备容器分组时返回的可移动功能。

PCI 总线驱动程序通过读取以下 PCIe 寄存器位来确定 PCIe 设备是否可移动。

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
<td align="left"><p>已实现8槽</p></td>
<td align="left"><p>设置为1时，此位值指示与此端口关联的 PCIe 链接连接到物理槽，而不是连接到集成组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>槽功能</p></td>
<td align="left"><p>0x14</p></td>
<td align="left"><p>6-Hot-Plug 支持</p></td>
<td align="left"><p>当设置为1时，此位值指示该槽可以支持热插操作。</p></td>
</tr>
</tbody>
</table>

 

如果满足以下两个条件，PCI 总线驱动程序会将 PCIe 设备标记为可移动设备：

-   槽实现的位设置为1。

-   支持热插拔的位设置为1：

用于设置这些寄存器位的机制因 PCIe 芯片芯片版本和制造商的不同而异。 例如，某些芯片组使固件编程这些位，而其他芯片集需要将物理 pin 现金不足到 (Vcc) 或地面 (GND) 的电压收费连接。

请注意，如果设备在 ACPI 命名空间中实现 _EJ0 方法，ACPI 驱动程序会将该设备标记为可移动设备。 无论实现的槽或 Hot-Plug 支持的位的设置如何都是如此。 有关详细信息，请参阅 [热插拔 PCI 和 Windows](https://go.microsoft.com/fwlink/p/?linkid=26278) 白皮书。

有关 PCIe 接口的详细信息，请参阅 [Pcie 基本](https://go.microsoft.com/fwlink/p/?linkid=69486) 规范。

 

 





