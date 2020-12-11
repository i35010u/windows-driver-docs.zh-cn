---
title: 按钮功能数组
description: 按钮功能数组
keywords:
- button 功能阵列 WDK HID
- 阵列 WDK HID
- 功能 WDK HID 集合
- 按钮用法 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7fc55b33d506c5a96bfc2baad0c6f66418d3514
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091114"
---
# <a name="button-capability-arrays"></a>按钮功能数组





*按钮功能数组* 包含有关特定类型的 HID 报表的 [顶级集合](top-level-collections.md)支持的按钮用法的信息。 有关集合功能的信息包含在其 [**HIDP \_ cap**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps) 结构中。

用户模式应用程序或内核模式驱动程序使用以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid) 之一获取按钮功能信息：

-   [**HidP \_GetButtonCaps**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps) 返回一个按钮功能数组，用于描述指定报表类型中包含的所有按钮用法。

-   [**HidP \_GetSpecificButtonCaps**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificbuttoncaps) 筛选由调用方指定的使用情况页、使用 ID 和 [链接集合](link-collections.md)返回的按钮功能信息。

按钮功能数组包含 [**HIDP \_ 按钮 \_ cap**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_button_caps) 结构，其中每个都包含有关 [HID 使用情况](hid-usages.md) 或 [使用范围](hid-usages.md#usage-range)的下列信息：

-   使用情况或使用情况范围的使用情况页

-   包含按钮数据的报表的报表 ID

-   使用 ID 或使用范围

-   一个标志，用于指示使用情况是否为[别名](hid-usages.md#aliased-usages)使用

-   包含用量或使用情况范围的链接集合

-   与用法或使用情况范围关联的字符串描述符和指示符 (参阅指示符索引项和字符串索引项) 

-   HID 分析器分配给使用情况或使用范围的[数据索引](data-indices.md)

一般情况下，下列条件适用于按钮功能数组描述的所有用法：

-   每个功能结构都表示一个与变量主项或数组主项相关联的使用情况或使用情况范围。

-   别名使用情况可与变量主项目一起使用。 与数组项关联的使用不能化名为别名。 使用范围不能有别名。

-   HID 分析器仅使用所需的最低数量的用法来向每个按钮分配使用情况。 分析器按在报表描述符中指定的顺序来分配使用情况。 不需要的报表描述符中的用法将被丢弃。 按钮功能数组不包含有关被丢弃的用法的任何信息。

-   如果为变量项指定的使用次数小于项中的按钮数，则该功能数组仅包含一个功能结构，该结构描述了) 的变量主项的报表描述符中指定的最后 (一个使用情况。 但是，有关报表计数大于1的使用值的信息，请参阅 [用量值数组](value-capability-arrays.md#usage-value-array) 。

-   HID 分析器为功能数组中所述的每个使用分配一个唯一的数据索引。

以下主题讨论如何在 button 功能数组中组织和设置功能结构：

[变量主项目中的按钮用法](#button-usages-in-a-variable-main-item)

[数组主项目中的按钮用法](#button-usages-in-an-array-main-item)

### <a name="button-usages-in-a-variable-main-item"></a><a href="" id="button-usages-in-a-variable-main-item"></a> 变量主项目中的按钮用法

在报表描述符中指定的每个 [使用情况](hid-usages.md) 或 [使用范围](hid-usages.md#usage-range) 由其在按钮功能数组中的功能结构描述。

功能结构的 " **IsAlias** " 成员用于指定一组 *n* 化名的用法，如下所示：

-   在添加到功能数组的前 *n* 个功能结构中， **IsAlias** 设置为 **TRUE** 。 在第 *n* 个功能结构中， **IsAlias** 设置为 **FALSE** 。 首选用法是序列中最后一个别名使用情况。

应用程序或驱动程序可以通过扫描此类序列来确定哪些按钮用法具有别名。

下表总结了三个化名使用的示例。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>报表描述符中的别名使用顺序</th>
<th>功能数组中的使用顺序</th>
<th>IsAlias 成员值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用量1</p></td>
<td><p>使用情况3</p></td>
<td><p><strong>TRUE</strong></p></td>
</tr>
<tr class="even">
<td><p>使用情况2</p></td>
<td><p>使用情况2</p></td>
<td><p><strong>TRUE</strong></p></td>
</tr>
<tr class="odd">
<td><p>使用情况3</p></td>
<td><p>使用量1</p></td>
<td><p><strong>FALSE</strong></p></td>
</tr>
</tbody>
</table>

 

有关如何交叉引用使用情况和数据索引的信息，请参阅 [数据索引](data-indices.md)。

### <a name="button-usages-in-an-array-main-item"></a><a href="" id="button-usages-in-an-array-main-item"></a> 数组主项目中的按钮用法

在报表描述符中指定的按钮数组主要项的每个 [使用情况](hid-usages.md) 或 [使用范围](hid-usages.md#usage-range) 均由其在按钮功能数组中的功能结构描述。 将功能结构添加到功能数组中的顺序与为主项目指定用法的顺序相反。

HID 分析器将 [数据索引](data-indices.md) 分配给与数组项关联的每个使用情况，并按报表描述符中指定用法的顺序排列。 例如，下表显示了在 "功能数组" 中指定的一组使用情况（在报表描述符中指定）和 "用法" 和 "数据" 索引之间的对应关系。 在此表中 (， *n* 是分析器分配给与数组项关联的第一个用法的第一个数据索引。 ) 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>报表描述符中的使用顺序</th>
<th>功能数组中的使用顺序</th>
<th>DataIndex 或从 DataIndexMin 到 DatatIndexMax</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用量1</p></td>
<td><p>使用范围2</p></td>
<td><p>从 <em>n</em>+ 7 到 <em>n</em>+ 8</p></td>
</tr>
<tr class="even">
<td><p>使用范围 1 (具有4个用法) </p></td>
<td><p>使用情况2</p></td>
<td><p><em>n</em>+ 5</p></td>
</tr>
<tr class="odd">
<td><p>使用情况2</p></td>
<td><p>使用范围1</p></td>
<td><p>从 <em>n</em>+ 1 到 <em>n</em>+ 4</p></td>
</tr>
<tr class="even">
<td><p>使用范围 2 (具有2个用法) </p></td>
<td><p>使用量1</p></td>
<td><p><em>n</em></p></td>
</tr>
</tbody>
</table>

 

 

