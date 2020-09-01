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
ms.openlocfilehash: 89f77d14a178a80afbd15baacdf26606af00938d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190611"
---
# <a name="connections-between-two-unit-plugs-in-different-avc-units"></a>在不同 AV/C 单元中的两个单元插头之间的连接


方案7和8表示一个单元中的子单位与不同单元中的子单位之间的连接，其中目标不支持一个 AV/C 单元内的单元连接。 这些类型的连接需要 **信号源** ，并 **输入** CCM 命令。

方案7和8描述了在其[**AVCPRECONNECTINFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)结构的**标志**成员中设置了**KSPIN \_ 标志 \_ AVC \_ PCRONLY**标志的子单位源或目标插头，该标志由*Avc.sys*转换为子地址的0xff。

### <a name="scenario-7"></a>**方案7**

**信号源**：本地单元不支持内部连接。

**输入选择**：本地单元从任何可用的 (0x7f) 目标单元连接到任何可用的 (0x7f) 本地单元上的任何可用的0x7f，然后连接到本地单元上的特定 () 子区域目标插件。

![演示本地 pin 的数据流成员在 kspin 的 \- 数据流中的连接的关系图 \-](images/avc-ccm7.gif)

方案7介绍了本地 pin 的 **数据流** 成员 \_ 在中 KSPIN 数据流的连接 \_ 。

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
<td><p>源插件 (0xFF) 已忽略值</p></td>
<td><p>0x0 到0x1E 或0xFF</p></td>
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
<td><p>目标插头 (0x0 到0x1E 或 0xFF) </p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-8"></a>**方案8**

**信号源**：本地单元连接到任何可用的 (0x7f) 按同步输出插件 (，并返回) 的同步输出插件的数字。

**输入选择**：目标单元从本地单元的同步输出插件连接 (在信号源 CCM 命令) 连接到任何可用的 (0x7f) 目标单元上的同步输入插件。

![说明本地 pin \- 的数据流成员 kspin 的连接的关系图 \-](images/avc-ccm8.gif)

方案8描述了一个连接，其中本地 pin 的 **数据流** 成员是 KSPIN \_ 数据流 \_ 。

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
<td><p>源插件 (0x0 到0x1E 或 0xFF) </p></td>
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
<td><p>已忽略目标插入 (0xFF) -值</p></td>
<td><p>0x0 到0x1E，或0x7F</p></td>
</tr>
</tbody>
</table>

 

以下列表描述了前面的表中显示的值的含义：

-   值0x0 到 0x1E (30 decimal) 表示特定的插件号。

-   值0x7F 表示 AV/C 单元上的任何可用的同步输入或输出插件号。

-   值0xFF 表示任意可用的子源或目标的插入地址。

-   "Self" 包含 AVCCONNECTINFO 结构所设置的 pin。 "Target" 表示 AVCCONNECTINFO 结构用于的数据。

-   为源和目标子源插入 (的 **DeviceID** 列中的值) 用于搜索目标 AV/c 设备的物理设备对象 (PDO) ，以向发出 AV/c CCM 命令。

 

