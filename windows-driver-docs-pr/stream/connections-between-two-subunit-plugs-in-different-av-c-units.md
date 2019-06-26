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
ms.openlocfilehash: cbdfeb5137670399a60b170dc936e2648619d475
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384499"
---
# <a name="connections-between-two-subunit-plugs-in-different-avc-units"></a>在不同 AV/C 单元中的两个子单元插头之间的连接


方案 5 和 6 表示为子单元不同单元中的一个单元中子单元之间的连接。 这些类型的连接需要**信号源**并**输入选择**CCM 命令。

### <a href="" id="scenario-5"></a> 方案 5

**信号源**:目标单元连接到特定的子单元源插件 (0x0 到 0x1E)，或任何可用的子单元源 (0xFF) 插入到特定的单元等时输出即插即用或任何可用单元等时输出插入 （并返回单元的同步输出的即插即用数字）。

**输入选择**:本地单元从目标子单元的源即插即用连接到任何本地单元等时输入插头，然后连接到任何可用的子单元目标即插即用。

![方案 5 子单元连接](images/avc-ccm5.gif)

方案 5 描述的连接的本地固定的**数据流**成员是 KSPIN\_数据流\_in。

下表中的每一列对应的成员[ **AVCCONNECTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avcconnectinfo)结构和源子单元即插即用这些成员中指定的值。

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
<th>UnitPlugNumber （对于同步输出）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>目标</p></td>
<td><p>子单元地址</p></td>
<td><p>（0x0 到 0x1E 或 0xFF） 源即插即用</p></td>
<td><p>0x0 到 0x1E 或 0x7F</p></td>
</tr>
</tbody>
</table>

 

下表中的每列对应于 AVCCONNECTINFO 结构的成员，这些成员的目标子单元即插即用指定的值。

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
<th>UnitPlugNumber （适用于同步输入）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self</p></td>
<td><p>Self</p></td>
<td><p>目标即插即用 (0xFF)</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="scenario-6"></a> 方案 6

**信号源**:本地单元连接到任何本地单元等时输出插入到任何可用 (0xFF) 子单元源即插即用 （并返回单元的同步输出的即插即用数字）。

**输入选择**:目标单元从本地设备的特定等时输出即插即用 （返回信号源 CCM 命令中） 连接到特定 (0x0 0x1E) 或任何可用的 (0x7F) 等时输入的目标单元上插入，然后连接到特定 (0x0 0x1E) 或任何可用 (0xFF) 子单元目标插入目标单元 （这种情况下为方案 5 相反）。

![方案 6 子单元连接](images/avc-ccm6.gif)

方案 6 描述的连接的本地固定的**数据流**成员是 KSPIN\_数据流\_出。

下表中的每列对应于 AVCCONNECTINFO 结构的成员，指定源子单元即插即用这些成员的值。

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
<th>UnitPlugNumber （对于同步输出）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self</p></td>
<td><p>Self</p></td>
<td><p>源即插即用 (0xFF)</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

下表中的每列对应于 AVCCONNECTINFO 结构的成员，这些成员的目标子单元即插即用指定的值。

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
<th>UnitPlugNumber （适用于同步输入）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>目标</p></td>
<td><p>子单元地址</p></td>
<td><p>目标即插即用 (0x0 0x1E)</p></td>
<td><p>0x0 到 0x1E 或 0x7F</p></td>
</tr>
</tbody>
</table>

 

以下列表说明了上述表中显示的值的含义：

-   值为 0x1E 0x0 (十进制 30) 表示特定的即插即用的数字。

-   0x7F 的值表示任何可用的同步输入或输出 AV/C 单元上的即插即用数字。

-   值 0xFF 代表任何可用的子单元源或目标插入地址。

-   "Self"包含 AVCCONNECTINFO 结构设置到的 pin。 "目标"表示 AVCCONNECTINFO 结构有关的数据。

-   中的值**设备 ID**列 （适用于源和目标子单元插头） 用于搜索的物理设备对象 (PDO) 要发出到 AV/C CCM 命令的目标 AV/C 设备。

 

 




