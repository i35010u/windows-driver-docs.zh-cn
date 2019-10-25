---
title: 一个 AV/C 单元中的子单位插头和单元插头之间的连接
description: 提供有关每个 AV/C 单位内的子单位插头与单元插头之间连接的信息
ms.assetid: 12132a0c-9657-4cff-a582-8404a103c46a
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- AVCCONNECTINFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ca02f7a8144e4ff1e0e4068add375241433e4bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844713"
---
# <a name="connections-between-subunit-plugs-and-unit-plugs-within-one-avc-unit"></a>一个 AV/C 单元中的子单位插头和单元插头之间的连接


方案1和2表示子单位与包含子单位的单位之间的连接。

### <a name="scenario-1"></a>**方案1**

如下图所示，将本地子源的源插件连接到设备的同步输出插件。

此方案是最初在*Avc*中支持的连接类型。

![演示本地 pin 的数据流成员在 kspin\-数据流的连接的关系图\-](images/avc-ccm1.gif)

方案1描述了一个连接，其中本地 pin 的**数据流**成员是在中 KSPIN\_数据流\_的。

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
<td><p>0xFF （包含子单位的单位）</p></td>
<td><p>iPlug （0x0 到0x1E 或0x7F）</p></td>
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
<td><p>目标插件（0x0 到0x1E）</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>

 

### <a name="scenario-2"></a>**方案2**

按下图所示，从单元的按下的输入插件连接到本地子区域的目标插件。

![说明本地 pin 的数据流成员 kspin\-数据流的连接的关系图\-](images/avc-ccm2.gif)

方案2描述了一个连接，其中本地 pin 的**数据流**成员是 KSPIN\_数据流\_的。

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
<td><p>子地址</p></td>
<td><p>源插件（0x0 到0x1E）</p></td>
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
<td><p>0xFF （包含子单位的单位）</p></td>
<td><p>oPCR （0x0 到0x1E，或0x7F）</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>

 

以下列表描述了前面的表中显示的值的含义：

-   值0x0 到0x1E （30 decimal）表示特定的插件号。

-   值0x7F 表示 AV/C 单元上的任何可用的同步输入或输出插件号。

-   值0xFF 表示任意可用的子源或目标的插入地址。

-   **DeviceID**列中的值（适用于源和目标子源插头）用于搜索目标 Av/c 设备的物理设备对象（PDO），以便向发出 AV/c CCM 命令。

 

 




