---
title: 按钮功能数组
description: 按钮功能数组
ms.assetid: 139324e5-4d46-4d00-9f5a-fd0313fc109a
keywords:
- WDK HID 按钮功能数组
- WDK HID 的数组
- 功能 WDK HID 集合
- WDK HID 按钮用途
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7f629555bf78105b0ad0f193b83eb88ee81b41b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521087"
---
# <a name="button-capability-arrays"></a>按钮功能数组





一个*按钮功能数组*包含有关支持的按钮使用情况的信息[顶级集合](top-level-collections.md)HID 报表为特定类型。 有关集合的功能的信息包含在其[ **HIDP\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539697)结构。

用户模式应用程序或内核模式驱动程序将使用以下值之一[HIDClass 支持例程](https://msdn.microsoft.com/library/windows/hardware/ff538865)获取按钮功能的信息：

-   [**HidP\_GetButtonCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff539707)返回描述指定的报表类型中包含的所有按钮用途的按钮功能数组。

-   [**HidP\_GetSpecificButtonCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff539733)筛选器按钮功能信息，它将返回调用方指定的使用情况页，使用 ID 和[集合链接](link-collections.md)。

按钮功能包含一个数组[ **HIDP\_按钮\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff539693)结构，其中每个包含以下信息有关[的HID用途](hid-usages.md)或[使用范围](hid-usages.md#usage-range):

-   使用情况或使用范围的使用情况页面

-   包含按钮数据的报表的报表 ID

-   使用 ID 或使用范围

-   一个标志，指示是否存在此用法的[别名使用情况](hid-usages.md#aliased-usages)

-   包含的使用情况或使用范围的链接集合

-   字符串描述符和使用情况或使用区域相关联的指示符 （请参阅指示符索引项和字符串索引项）

-   [数据索引](data-indices.md)HID 分析器分配给使用情况或使用范围

一般情况下，描述按钮功能数组的所有用法都具备以下条件：

-   每个功能结构表示单一的使用情况或与变量的主要项或数组主要项相关联的使用范围。

-   使用别名用法可以在变量的主要项。 与数组项相关联的使用情况不能有别名。 使用范围不能有别名。

-   HID 分析器使用只有使用实例的最小所需的数量将用量分配给每个按钮。 分析器将分配的报告描述符中指定的顺序的用法。 不是必需的报表描述符中使用实例将被丢弃。 按钮功能数组不包含任何有关放弃用法的信息。

-   功能数组的用法指定为变量的项目数小于项中的按钮数，如果包含只有一个功能结构，它描述了一个按钮用法 （最后一个指定的用法中主要的变量的报告描述符项）。 但是，请参阅[用法值数组](value-capability-arrays.md#usage-value-array)有关用法的信息有一个报表的值计数大于 1。

-   HID 分析器将分配给每个功能数组中所述的使用情况的唯一数据索引。

以下主题讨论如何组织和按钮功能阵列中设置的功能结构：

[变量的主要项中的按钮用途](#button-usages-in-a-variable-main-item)

[数组主要项中的按钮用途](#button-usages-in-an-array-main-item)

### <a href="" id="button-usages-in-a-variable-main-item"></a> 变量的主要项中的按钮用途

每个[使用情况](hid-usages.md)或[用法范围](hid-usages.md#usage-range)指定按钮功能数组中其自身功能结构描述符描述在报表中。

**IsAlias**功能结构的成员将用来指定一组*n*别名用法，如下所示：

-   **IsAlias**设置为**TRUE**在第一个*n*-1 功能添加到功能数组的结构。 **IsAlias**设置为**FALSE**中*n*th 功能结构。 首选的用法是在序列中的最后一个别名使用情况。

应用程序或驱动程序可以确定哪个按钮用途是通过扫描此类序列的别名。

下表总结了三个别名用法示例。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>使用别名使用情况报告描述符中的顺序</th>
<th>使用情况功能数组中的顺序</th>
<th>IsAlias 成员值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用情况 1</p></td>
<td><p>使用情况 3</p></td>
<td><p><strong>TRUE</strong></p></td>
</tr>
<tr class="even">
<td><p>使用情况 2</p></td>
<td><p>使用情况 2</p></td>
<td><p><strong>TRUE</strong></p></td>
</tr>
<tr class="odd">
<td><p>使用情况 3</p></td>
<td><p>使用情况 1</p></td>
<td><p><strong>FALSE</strong></p></td>
</tr>
</tbody>
</table>

 

有关如何使用实例和数据的索引的交叉引用的信息，请参阅[数据索引](data-indices.md)。

### <a href="" id="button-usages-in-an-array-main-item"></a> 数组主要项中的按钮用途

每个[使用情况](hid-usages.md)或[用法范围](hid-usages.md#usage-range)对于在报表中所指定的按钮数组主要项描述符描述按钮功能数组中其自身功能结构。 功能结构添加到功能数组中的顺序就是顺序的在其中指定主要项用法相反。

HID 分析器将分配[数据索引](data-indices.md)到每个数组项中的用法指定报表描述符中的顺序与相关联的使用情况。 例如下, 表显示了使用情况，是报表的描述符，和使用情况中指定一组和数据索引，指定功能数组中的对应关系。 (在此表中， *n*是分析器将分配给数组项与相关联的第一个应用的第一个数据索引。)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>使用情况报告描述符中的顺序</th>
<th>使用情况功能数组中的顺序</th>
<th>DataIndex 或从到 DatatIndexMax DataIndexMin</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用情况 1</p></td>
<td><p>使用范围 2</p></td>
<td><p>从<em>n</em>到 + 7 <em>n</em>+ 8</p></td>
</tr>
<tr class="even">
<td><p>使用范围 1 （具有 4 个用法）</p></td>
<td><p>使用情况 2</p></td>
<td><p><em>n</em>+5</p></td>
</tr>
<tr class="odd">
<td><p>使用情况 2</p></td>
<td><p>使用范围 1</p></td>
<td><p>从<em>n</em>+ 1 到<em>n</em>+ 4</p></td>
</tr>
<tr class="even">
<td><p>（使用 2 个用法） 的使用情况范围 2</p></td>
<td><p>使用情况 1</p></td>
<td><p><em>n</em></p></td>
</tr>
</tbody>
</table>

 

 

 




