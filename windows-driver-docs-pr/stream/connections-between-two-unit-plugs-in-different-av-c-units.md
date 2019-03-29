---
title: 在不同 AV/C 单元中的两个单元插头之间的连接
description: 在不同 AV/C 单元中的两个单元插头之间的连接
ms.assetid: b9c45304-33a2-4d02-9c38-1d124a33f0f2
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- AVCCONNECTINFO
- AVCPRECONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93d1fe5bc36ab8aa7281fadfae1cd2275784935f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567098"
---
# <a name="connections-between-two-unit-plugs-in-different-avc-units"></a>在不同 AV/C 单元中的两个单元插头之间的连接


方案 7 和 8 表示为在不同单元中，目标不支持一个 AV/C 单元内的单元连接到的子单元子单元的一个单元中子单元之间的连接。 这些类型的连接需要**信号源**并**输入选择**CCM 命令。

方案 7 和 8 描述具有的子单元源或目标插头**KSPIN\_标志\_AVC\_PCRONLY**中设置标志**标志**其的成员[**AVCPRECONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554103)结构转换*Avc.sys*到 0xFF 及其子单元的地址。

### <a name="scenario-7"></a>**方案 7**

**信号源**:本地单元不支持内部单元连接。

**输入选择**:本地单元从目标设备上的任何可用 (0x7F) 等时输出即插即用连接到任何可用 (0x7F) 等时输入即插即用本地设备上，然后连接到特定 (0x0 0x1E) 或任何可用的 (0xFF) 子单元目标插入本地单元.

![关系图说明如何的连接本地 pin 数据流成员所在 kspin\-数据流\-中](images/avc-ccm7.gif)

方案 7 描述了其中本地固定的连接的**数据流**成员是 KSPIN\_数据流\_in。

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
<td><p>目标</p></td>
<td><p>子单元地址</p></td>
<td><p>源即插即用 (0xFF) 的值将被忽略</p></td>
<td><p>0x0 到 0x1E 或 0xFF</p></td>
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
<td><p>（0x0 到 0x1E 或 0xFF） 目标即插即用</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-8"></a>**方案 8**

**信号源**:本地单元连接到任何子单元的源即插即用到任何可用 (0x7F) 等时输出即插即用 （并返回同步的输出插件的数目）。

**输入选择**:目标单元从本地单元等时输出即插即用 （返回信号源 CCM 命令中） 连接到任何可用 (0x7F) 等时输入即插即用的目标单元上。

![关系图说明如何的连接本地 pin 数据流成员所在 kspin\-数据流\-出](images/avc-ccm8.gif)

方案 8 描述的连接的本地固定的**数据流**成员是 KSPIN\_数据流\_出。

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
<td><p>（0x0 到 0x1E 或 0xFF） 源即插即用</p></td>
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
<td><p>目标插入 (0xFF)-将忽略值</p></td>
<td><p>0x0 到 0x1E 或 0x7F</p></td>
</tr>
</tbody>
</table>

 

以下列表说明了上述表中显示的值的含义：

-   值为 0x1E 0x0 (十进制 30) 表示特定的即插即用的数字。

-   0x7F 的值表示任何可用的同步输入或输出 AV/C 单元上的即插即用数字。

-   值 0xFF 代表任何可用的子单元源或目标插入地址。

-   "Self"包含 AVCCONNECTINFO 结构设置到的 pin。 "目标"表示 AVCCONNECTINFO 结构有关的数据。

-   中的值**DeviceID**列 （适用于源和目标子单元插头） 用于搜索的物理设备对象 (PDO) 要发出到 AV/C CCM 命令的目标 AV/C 设备。

 

 




