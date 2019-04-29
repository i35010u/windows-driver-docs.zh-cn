---
title: 在一个 AV/C 单元中的两个子单元插头之间的连接
description: 提供一个 AV/C 单位内的两个子单元插入之间的连接信息
ms.assetid: 2acd5f23-89b6-40f9-9154-22f1bb51d08c
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186401f7636f93bb77fdc5fd090fad8749110425
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374242"
---
# <a name="connections-between-two-subunit-plugs-within-one-avc-unit"></a>在一个 AV/C 单元中的两个子单元插头之间的连接


方案 3 和 4 代表子单元和相同单元中的另一个子单元之间的连接。

### <a name="scenario-3"></a>**方案 3**

从特定源即插即用 (0x0 到 0x1E)，连接或任何可用的源插入 (0xFF) 的另一个子单元在相同单元中，为本地子单元的目标即插即用，如下图所示显示。

![关系图说明如何的连接本地 pin 数据流成员所在 kspin\-数据流\-中](images/avc-ccm3.gif)

方案 3 介绍了本地固定的其中一个连接的**数据流**成员是 KSPIN\_数据流\_in。

下表中的每一列对应的成员[ **AVCCONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554101)结构和源子单元即插即用这些成员中指定的值。

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
<td><p>不使用，因为源设备的设备标识符是单元，其中包含子单元</p></td>
<td><p>子单元地址</p></td>
<td><p>（0x0 到 0x1E 或 0xFF） 目标即插即用</p></td>
<td><p>不可用</p></td>
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
<td><p>不使用，因为这种情况下不涉及另一个单元</p></td>
<td><p>Self</p></td>
<td><p>目标即插即用 (0xFF)</p></td>
<td><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-4"></a>**方案 4**

从本地子单元的源即插即用到特定的目标即插即用 (0x0 到 0x1E) 或任何可用 (0xFF) 目标即插即用的另一个子单元连接，如下图所示。 方案 4 表示方案 3 相反。

![关系图说明如何的连接本地 pin 数据流成员所在 kspin\-数据流\-出](images/avc-ccm4.gif)

方案 4 描述的连接的本地固定的**数据流**成员是 KSPIN\_数据流\_出。

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
<td><p>不使用，因为源设备的设备标识符是单元，其中包含子单元</p></td>
<td><p>Self （相同子单元）</p></td>
<td><p>源即插即用 (0xFF)</p></td>
<td><p>不可用</p></td>
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
<td><p>不使用，因为这种情况下不涉及另一个单元</p></td>
<td><p>子单元地址</p></td>
<td><p>（0x0 到 0x1E 或 0xFF） 目标即插即用</p></td>
<td><p>不可用</p></td>
</tr>
</tbody>
</table>

 

以下列表说明了上述表中显示的值的含义：

-   值为 0x1E 0x0 (十进制 30) 表示特定的即插即用的数字。

-   值 0xFF 代表任何可用的子单元源或目标插入地址。

-   "Self"包含 AVCCONNECTINFO 结构设置到的 pin。

-   中的值**DeviceID**列 （适用于源和目标子单元插头） 用于搜索的物理设备对象 (PDO) 要发出到 AV/C CCM 命令的目标 AV/C 设备。

 

 




