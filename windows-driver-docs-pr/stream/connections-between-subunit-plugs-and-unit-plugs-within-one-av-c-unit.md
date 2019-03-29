---
title: 子单元插入和一个 AV/C 单位内的单元插入之间的连接
description: 提供有关子单元插入和一个 AV/C 单位内的单元插入之间的连接信息
ms.assetid: 12132a0c-9657-4cff-a582-8404a103c46a
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33da5a4d4cdc15be31aae2c7eb21593a941e8003
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348962"
---
# <a name="connections-between-subunit-plugs-and-unit-plugs-within-one-avc-unit"></a>子单元插入和一个 AV/C 单位内的单元插入之间的连接


方案 1 和 2 代表包含子单元的单元的子单元之间的连接。

### <a name="scenario-1"></a>**方案 1**

连接本地子单元的源即插即用到的单元等时输出即插即用，如下图所示。

此方案是在最初支持的连接的类型*Avc.sys*。

![关系图说明如何的连接本地 pin 数据流成员所在 kspin\-数据流\-中](images/avc-ccm1.gif)

方案 1 描述的连接的本地固定的**数据流**成员是 KSPIN\_数据流\_in。

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
<td><p>0xFF （包含的单元的子单元）</p></td>
<td><p>iPlug （0x0 到 0x1E 或 0x7F）</p></td>
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
<td><p>目标即插即用 (0x0 0x1E)</p></td>
<td><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-2"></a>**方案 2**

如下图所示的单元等时输入插件从连接到本地子单元的目标即插即用。

![关系图说明如何的连接本地 pin 数据流成员所在 kspin\-数据流\-出](images/avc-ccm2.gif)

方案 2 描述的连接的本地固定的**数据流**成员是 KSPIN\_数据流\_出。

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
<td><p>子单元地址</p></td>
<td><p>源即插即用 (0x0 0x1E)</p></td>
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
<td><p>0xFF （包含子单元的单元）</p></td>
<td><p>oPCR （0x0 到 0x1E 或 0x7F）</p></td>
<td><p>不可用</p></td>
</tr>
</tbody>
</table>

 

以下列表说明了上述表中显示的值的含义：

-   值为 0x1E 0x0 (十进制 30) 表示特定的即插即用的数字。

-   0x7F 的值表示任何可用的同步输入或输出 AV/C 单元上的即插即用数字。

-   值 0xFF 代表任何可用的子单元源或目标插入地址。

-   中的值**DeviceID**列 （适用于源和目标子单元插头） 用于搜索的物理设备对象 (PDO) 要发出到 AV/C CCM 命令的目标 AV/C 设备。

 

 




