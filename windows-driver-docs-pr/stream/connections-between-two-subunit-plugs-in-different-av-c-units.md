---
title: 在不同 AV/C 单元中的两个子单元插头之间的连接
description: 在不同 AV/C 单元中的两个子单元插头之间的连接
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c265e20a2eb304ecf39641ffbe572f0dd398841a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795855"
---
# <a name="connections-between-two-subunit-plugs-in-different-avc-units"></a>在不同 AV/C 单元中的两个子单元插头之间的连接


方案5和6表示一个单元中的子单位与不同单元中的子单位之间的连接。 这些类型的连接需要 **信号源** ，并 **输入** CCM 命令。

### <a name="scenario-5"></a><a href="" id="scenario-5"></a> 方案5

**信号源**：目标单元连接到特定的子源源插头 (0X0 到 0x1E) ，或任意可用的子源插件 (0xff) ，到特定的单元同步输出插件，或任何可用的单元同步输出插件 (并返回单元的同步输出插件) 。

**输入选择**：本地单元从目标子源的源插件连接到本地单位的任何同步输入插头，然后连接到任何可用的子源目标插件。

![方案5子单位连接](images/avc-ccm5.gif)

方案5描述了一个连接，其中本地 pin 的 **数据流** 成员是 \_ 中的 KSPIN 数据流 \_ 。

下表中的每列对应于 [**AVCCONNECTINFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo) 结构的成员，并为源子源插件的这些成员指定值。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceID</th>
<th>SubunitAddress</th>
<th>SubunitPlugNumber</th>
<th>同步输出的 UnitPlugNumber () </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>目标</p></td>
<td><p>子地址</p></td>
<td><p>源插件 (0x0 到0x1E 或 0xFF) </p></td>
<td><p>0x0 到0x1E，或0x7F</p></td>
</tr>
</tbody>
</table>

 

下表中的每一列对应于 AVCCONNECTINFO 结构的成员，并为这些成员指定了目标子单位插件的值。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceID</th>
<th>SubunitAddress</th>
<th>SubunitPlugNumber</th>
<th>同步输入的 UnitPlugNumber () </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>自己</p></td>
<td><p>自己</p></td>
<td><p>目标插头 (0xFF) </p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-6"></a><a href="" id="scenario-6"></a> 方案6

**信号源**：本地单元连接到任何可用 (0xff) 子源插件发送到本地单元的任何同步输出插件 (，并返回单元的同步输出插件号) 。

**输入选择**：目标单元从本地单元的特定 (的同步输出插件连接到) 到特定 (0x0 的特定0x0，并) 将目标单元上的任何可用 (0x7f) 同步输入插件，然后连接到特定的 (0X0 到 0x1E) 或任何可用的 (0xff) 目标单元。

![方案6子单位连接](images/avc-ccm6.gif)

方案6描述了一个连接，其中本地 pin 的 **数据流** 成员是 KSPIN \_ 数据流 \_ 。

下表中的每列对应于 AVCCONNECTINFO 结构的成员，并为源子源插件的这些成员指定值。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceID</th>
<th>SubunitAddress</th>
<th>SubunitPlugNumber</th>
<th>同步输出的 UnitPlugNumber () </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>自己</p></td>
<td><p>自己</p></td>
<td><p>源插件 (0xFF) </p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

下表中的每一列对应于 AVCCONNECTINFO 结构的成员，并为这些成员指定了目标子单位插件的值。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>DeviceID</th>
<th>SubunitAddress</th>
<th>SubunitPlugNumber</th>
<th>同步输入的 UnitPlugNumber () </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>目标</p></td>
<td><p>子地址</p></td>
<td><p>目标插头 (0x0 到 0x1E) </p></td>
<td><p>0x0 到0x1E，或0x7F</p></td>
</tr>
</tbody>
</table>

 

以下列表描述了前面的表中显示的值的含义：

-   值0x0 到 0x1E (30 decimal) 表示特定的插件号。

-   值0x7F 表示 AV/C 单元上的任何可用的同步输入或输出插件号。

-   值0xFF 表示任意可用的子源或目标的插入地址。

-   "Self" 包含 AVCCONNECTINFO 结构所设置的 pin。 "Target" 表示 AVCCONNECTINFO 结构用于的数据。

-   源和目标子源的 " **设备 ID** " 列 (中的值) 用于搜索目标 AV/c 设备的物理设备对象 (PDO) ，以向发出 AV/c CCM 命令。

 

