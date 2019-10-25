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
ms.openlocfilehash: 06e889459dc78b223c6ace0cc8866b0007e9492c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844706"
---
# <a name="connections-between-two-unit-plugs-in-different-avc-units"></a>在不同 AV/C 单元中的两个单元插头之间的连接


方案7和8表示一个单元中的子单位与不同单元中的子单位之间的连接，其中目标不支持一个 AV/C 单元内的单元连接。 这些类型的连接需要**信号源**，并**输入**CCM 命令。

方案7和8描述了具有 KSPIN\_标志的次级源或目标插头 **\_AVC\_PCRONLY**标志设置在其[**AVCPRECONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)结构的**标志**成员中，该标志由*AVC 转换*到0xff 的子地址。

### <a name="scenario-7"></a>**方案7**

**信号源**：本地单元不支持内部连接。

**输入选择**：本地单元从目标单元上的任何可用的（0x7f）同步输出插件连接到本地单元上任何可用的（0x7f）同步输入插件，然后连接到特定（0X0 到0x1E）或任何可用（0xff）子单位本地单元的目标插件。

![演示本地 pin 的数据流成员在 kspin\-数据流的连接的关系图\-](images/avc-ccm7.gif)

方案7描述了一个连接，其中本地 pin 的**数据流**成员是在中 KSPIN\_数据流\_的。

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
<td><p>已忽略源插件（0xFF）值</p></td>
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
<th>UnitPlugNumber （用于同步输入）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Self</p></td>
<td><p>Self</p></td>
<td><p>目标插件（0x0 到0x1E，即0xFF）</p></td>
<td><p>0x7F</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-8"></a>**方案8**

**信号源**：本地单元连接到任何可用的（0x7f）同步输出插件（并返回按同步输出插件的数字）。

**输入选择**：目标单元从本地单元的同步输出插件（在信号源 CCM 命令中返回）连接到目标单元上任何可用的（0x7f）同步输入插件。

![说明本地 pin 的数据流成员 kspin\-数据流的连接的关系图\-](images/avc-ccm8.gif)

方案8描述了一个连接，其中本地 pin 的**数据流**成员是 KSPIN\_数据流\_的。

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
<td><p>源插件（0x0 到0x1E，即0xFF）</p></td>
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
<td><p>已忽略目标插件（0xFF）-值</p></td>
<td><p>0x0 到0x1E，或0x7F</p></td>
</tr>
</tbody>
</table>

 

以下列表描述了前面的表中显示的值的含义：

-   值0x0 到0x1E （30 decimal）表示特定的插件号。

-   值0x7F 表示 AV/C 单元上的任何可用的同步输入或输出插件号。

-   值0xFF 表示任意可用的子源或目标的插入地址。

-   "Self" 包含 AVCCONNECTINFO 结构所设置的 pin。 "Target" 表示 AVCCONNECTINFO 结构用于的数据。

-   **DeviceID**列中的值（适用于源和目标子源插头）用于搜索目标 Av/c 设备的物理设备对象（PDO），以便向发出 AV/c CCM 命令。

 

 




