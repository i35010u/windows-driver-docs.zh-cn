---
title: 在一个 AV/C 单元中的两个子单元插头之间的连接
description: 提供有关一个 AV/C 单元内两个子单位插头之间连接的信息
ms.assetid: 2acd5f23-89b6-40f9-9154-22f1bb51d08c
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b3bfc26963b23af8d928e0701fdee1c3682e9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844708"
---
# <a name="connections-between-two-subunit-plugs-within-one-avc-unit"></a>在一个 AV/C 单元中的两个子单元插头之间的连接


方案3和4表示同一单元中的子单位和其他子单位之间的连接。

### <a name="scenario-3"></a>**方案3**

从特定的源插件（0x0 到0x1E）或同一单元中另一个子位置的任何可用源插件（0xFF）连接到本地子区域的目标插件，如下图所示。

![演示本地 pin 的数据流成员在 kspin\-数据流的连接的关系图\-](images/avc-ccm3.gif)

方案3描述了一个连接，其中本地 pin 的**数据流**成员是在中 KSPIN\_数据流\_的。

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
<td><p>未使用，因为源单元的设备标识符是包含子单位的单位</p></td>
<td><p>子地址</p></td>
<td><p>目标插件（0x0 到0x1E，即0xFF）</p></td>
<td><p>N/A</p></td>
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
<td><p>未使用，因为此方案不涉及其他单元</p></td>
<td><p>Self</p></td>
<td><p>目标插件（0xFF）</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-4"></a>**方案4**

从本地子源的源插件连接到特定的目标插头（0x0 到0x1E），或从另一个次级的任何可用（0xFF）目标插件进行连接，如下图所示。 方案4表示与方案3相反的情况。

![说明本地 pin 的数据流成员 kspin\-数据流的连接的关系图\-](images/avc-ccm4.gif)

方案4描述了一个连接，其中本地 pin 的**数据流**成员是 KSPIN\_数据流\_的。

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
<td><p>未使用，因为源单元的设备标识符是包含子单位的单位</p></td>
<td><p>自助（同一子单位）</p></td>
<td><p>源插件（0xFF）</p></td>
<td><p>N/A</p></td>
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
<td><p>未使用，因为此方案不涉及其他单元</p></td>
<td><p>子地址</p></td>
<td><p>目标插件（0x0 到0x1E，即0xFF）</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>

 

以下列表描述了前面的表中显示的值的含义：

-   值0x0 到0x1E （30 decimal）表示特定的插件号。

-   值0xFF 表示任意可用的子源或目标的插入地址。

-   "Self" 包含 AVCCONNECTINFO 结构所设置的 pin。

-   **DeviceID**列中的值（适用于源和目标子源插头）用于搜索目标 Av/c 设备的物理设备对象（PDO），以便向发出 AV/c CCM 命令。

 

 




