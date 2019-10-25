---
title: 在不同 AV/C 单元中的两个子单元插头之间的连接
description: 在不同 AV/C 单元中的两个子单元插头之间的连接
ms.assetid: 20d209b3-2516-4913-9f31-b14afddb78fb
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e6864ef9ec80829e31de5d30fcf84edfafcc010
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842429"
---
# <a name="connections-between-two-subunit-plugs-in-different-avc-units"></a>在不同 AV/C 单元中的两个子单元插头之间的连接


方案5和6表示一个单元中的子单位与不同单元中的子单位之间的连接。 这些类型的连接需要**信号源**，并**输入**CCM 命令。

### <a href="" id="scenario-5"></a>方案5

**信号源**：目标单元连接到特定的子源源插件（0X0 到0x1E），或任意可用的子源源插件（0xff）、特定单元的同步输出插件或任意可用的单元同步输出插件（并返回单元的同步输出插件号）。

**输入选择**：本地单元从目标子源的源插件连接到本地单位的任何同步输入插头，然后连接到任何可用的子源目标插件。

![方案5子单位连接](images/avc-ccm5.gif)

方案5描述了一个连接，其中本地 pin 的**数据流**成员是在中 KSPIN\_数据流\_的。

下表中的每列对应于[**AVCCONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)结构的成员，并为源子源插件的这些成员指定值。

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
<th>UnitPlugNumber （用于同步输出）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>目标</p></td>
<td><p>子地址</p></td>
<td><p>源插件（0x0 到0x1E，即0xFF）</p></td>
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
<th>UnitPlugNumber （用于同步输入）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self</p></td>
<td><p>Self</p></td>
<td><p>目标插件（0xFF）</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="scenario-6"></a>方案6

**信号源**：本地单元连接到任何本地单元的同步输出插件的任何可用（0xff）子源源插件（并返回单元的同步输出插件号）。

**输入选择**：目标单元从本地单元的特定同步输出插件（在信号源 CCM 命令中返回）连接到特定（0X0 到0x1E）或任何可用的（0x7f）按目标单元的输入插件，然后连接到特定（从0x0 到0x1E）或任何可用（0xFF） "目标单元" 的任何可用（0xFF）子区域目标插件（此方案与方案5相反）。

![方案6子单位连接](images/avc-ccm6.gif)

方案6描述了一个连接，其中本地 pin 的**数据流**成员是 KSPIN\_数据流\_的。

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
<th>UnitPlugNumber （用于同步输出）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self</p></td>
<td><p>Self</p></td>
<td><p>源插件（0xFF）</p></td>
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
<th>UnitPlugNumber （用于同步输入）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>目标</p></td>
<td><p>子地址</p></td>
<td><p>目标插件（0x0 到0x1E）</p></td>
<td><p>0x0 到0x1E，或0x7F</p></td>
</tr>
</tbody>
</table>

 

以下列表描述了前面的表中显示的值的含义：

-   值0x0 到0x1E （30 decimal）表示特定的插件号。

-   值0x7F 表示 AV/C 单元上的任何可用的同步输入或输出插件号。

-   值0xFF 表示任意可用的子源或目标的插入地址。

-   "Self" 包含 AVCCONNECTINFO 结构所设置的 pin。 "Target" 表示 AVCCONNECTINFO 结构用于的数据。

-   **设备 ID**列中的值（适用于源和目标子源插头）用于搜索目标 Av/c 设备的物理设备对象（PDO），以便向发出 AV/c CCM 命令。

 

 




