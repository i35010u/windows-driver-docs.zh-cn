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
ms.openlocfilehash: 225c00256a3428a03eaa5f98768ea003cf935d7e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190635"
---
# <a name="connections-between-two-subunit-plugs-within-one-avc-unit"></a>在一个 AV/C 单元中的两个子单元插头之间的连接


方案3和4表示同一单元中的子单位和其他子单位之间的连接。

### <a name="scenario-3"></a>**方案 3**

从特定的源插件 (0x0 连接到 0x1E) ，或同一单元中另一个子位置的任何可用源插件 (0xFF) ，如下图所示。

![演示本地 pin 的数据流成员在 kspin 的 \- 数据流中的连接的关系图 \-](images/avc-ccm3.gif)

方案3描述了一个连接，其中本地 pin 的 **数据流** 成员是 \_ 中的 KSPIN 数据流 \_ 。

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
<td><p>未使用，因为源单元的设备标识符是包含子单位的单位</p></td>
<td><p>子地址</p></td>
<td><p>目标插头 (0x0 到0x1E 或 0xFF) </p></td>
<td><p>不适用</p></td>
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
<td><p>未使用，因为此方案不涉及其他单元</p></td>
<td><p>自己</p></td>
<td><p>目标插头 (0xFF) </p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-4"></a>**方案 4**

从本地子源的源插头连接到特定的目标插头 (0x0 到 0x1E) ，或者从另一个子位置的任何可用的 (0xFF) 目标插头进行连接，如下图所示。 方案4表示与方案3相反的情况。

![说明本地 pin \- 的数据流成员 kspin 的连接的关系图 \-](images/avc-ccm4.gif)

方案4描述了一个连接，其中本地 pin 的 **数据流** 成员是 KSPIN \_ 数据流 \_ 。

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
<td><p>未使用，因为源单元的设备标识符是包含子单位的单位</p></td>
<td><p>自行 (相同的子) </p></td>
<td><p>源插件 (0xFF) </p></td>
<td><p>不适用</p></td>
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
<td><p>未使用，因为此方案不涉及其他单元</p></td>
<td><p>子地址</p></td>
<td><p>目标插头 (0x0 到0x1E 或 0xFF) </p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>

 

以下列表描述了前面的表中显示的值的含义：

-   值0x0 到 0x1E (30 decimal) 表示特定的插件号。

-   值0xFF 表示任意可用的子源或目标的插入地址。

-   "Self" 包含 AVCCONNECTINFO 结构所设置的 pin。

-   为源和目标子源插入 (的 **DeviceID** 列中的值) 用于搜索目标 AV/c 设备的物理设备对象 (PDO) ，以向发出 AV/c CCM 命令。

 

