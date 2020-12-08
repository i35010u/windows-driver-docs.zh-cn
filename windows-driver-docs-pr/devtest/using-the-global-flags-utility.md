---
title: 使用全局标志实用工具
description: 使用全局标志实用工具
keywords:
- 全局标志实用工具
- 驱动程序验证程序 WDK，全局标志实用工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ff4fa6276d52802895f568f14f835981b4a4e39
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803945"
---
# <a name="using-the-global-flags-utility"></a>使用全局标志实用工具


## <span id="ddk_using_the_global_flags_utility_tools"></span><span id="DDK_USING_THE_GLOBAL_FLAGS_UTILITY_TOOLS"></span>


全局标志 ( # A0) 实用程序提供了一种简单的方法，可在系统注册表中设置特定的密钥、调整正在运行的系统的内核设置，以及更改图像文件的设置。 可以通过使用图形或命令行界面来设置这些密钥。

全局标志实用程序可在 Windows 支持工具包和 Windows 的调试工具包中找到。 有关后者的详细信息，请参阅 [Windows 调试](../debugger/index.md)。

全局标志实用程序还可用于配置驱动程序验证程序的特殊池选项，或指定用于单个内存分配的特殊池。

若要更改特殊池设置，请启动 "全局标志" 实用工具，然后选择 "**目标**" 部分中的 "**系统注册表**" 选项按钮。 此对话框的 " **内核特殊池标记** " 部分允许设置某些特殊的池选项。

### <a name="span-idcontrolling_pool_tag_alignmentspanspan-idcontrolling_pool_tag_alignmentspancontrolling-pool-tag-alignment"></a><span id="controlling_pool_tag_alignment"></span><span id="CONTROLLING_POOL_TAG_ALIGNMENT"></span>控制池标记对齐

选择 " **验证启动** " 选项按钮，使特殊的池对齐方式专注于未检测到的检测。 选择 " **验证结束** " 选项以关注超限检测。 这些按钮控制所有特殊池分配的对齐方式，无论是由驱动程序验证程序还是由全局标志进行。

### <a name="span-idusing_special_pool_by_pool_tag_or_allocation_sizespanspan-idusing_special_pool_by_pool_tag_or_allocation_sizespanusing-special-pool-by-pool-tag-or-allocation-size"></a><span id="using_special_pool_by_pool_tag_or_allocation_size"></span><span id="USING_SPECIAL_POOL_BY_POOL_TAG_OR_ALLOCATION_SIZE"></span>按池标记或分配大小使用特殊池

特殊池可用于具有特定池标记的所有分配。 若要激活此功能，请将池标记输入到 " **池标记** " 文本框中。

特殊池还可用于特定大小范围内的所有分配。 虽然这种特殊的使用池不涉及池标记，但是，通过在 " **池标记** " 文本框中输入一个数字，仍会激活此功能。 此数字必须小于页面 \_ 大小。

对于 x86 处理器，页面 \_ 大小为0x1000，分配大小范围为8个字节。 若要为此范围内所有大小的分配激活特殊池，请输入一个等于此范围的最大值加上8的数字。  (此数字始终为8的倍数。 ) 下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">在 "池标记" 文本框中输入此编号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1到8个字节</p></td>
<td align="left"><p>16 (0x10) </p></td>
</tr>
<tr class="even">
<td align="left"><p>9到16字节</p></td>
<td align="left"><p>24 (0x18) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>17到24字节</p></td>
<td align="left"><p>32 (0x20) </p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFE9 to 0xFF0 bytes</p></td>
<td align="left"><p>0xFF8</p></td>
</tr>
</tbody>
</table>

 

对于 x64 处理器，页 \_ 大小为0x1000，分配大小范围是16个字节。 若要为此范围内所有大小的分配激活特殊池，请输入一个等于此范围的最大值加16的数字。  (此数字始终为16的倍数。 ) 下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">在 "池标记" 文本框中输入此编号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1到16字节</p></td>
<td align="left"><p>32 (0x20) </p></td>
</tr>
<tr class="even">
<td align="left"><p>17到32字节</p></td>
<td align="left"><p>48 (0x30) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>33到48字节</p></td>
<td align="left"><p>64 (0x40) </p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFD1 to 0xFE0 bytes</p></td>
<td align="left"><p>0xFF0</p></td>
</tr>
</tbody>
</table>

 

对于基于 Itanium 的处理器，页面 \_ 大小为0x2000，分配大小范围是16个字节。 若要为此范围内所有大小的分配激活特殊池，请输入一个等于此范围的最大值加16的数字。  (此数字始终为16的倍数。 ) 下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">在 "池标记" 文本框中输入此编号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1到16字节</p></td>
<td align="left"><p>32 (0x20) </p></td>
</tr>
<tr class="even">
<td align="left"><p>17到32字节</p></td>
<td align="left"><p>48 (0x30) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>33到48字节</p></td>
<td align="left"><p>64 (0x40) </p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1FD1 to 0x1FE0 bytes</p></td>
<td align="left"><p>0x1FF0</p></td>
</tr>
</tbody>
</table>

 

最好避免使用低于页面 \_ 大小的池标记。 例如，如果将0x30 放在基于 Itanium 的处理器上的此文本框中，则会将一个专用池用于大小介于17到32字节之间的所有分配，并用于包含池标记0x0030 的分配。

**注意**   如果驱动程序验证程序启用了驱动程序的特殊池，并且全局标志实用工具已为池标记或分配大小启用了特殊池，则会将此特殊池用于满足这些条件的所有分配 (受池可用性) 。

 

有关使用特殊池的完整详细信息，请参阅 [特殊池](special-pool.md) 。

 

