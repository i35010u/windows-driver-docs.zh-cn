---
title: 使用全局标志实用工具
description: 使用全局标志实用工具
ms.assetid: 934272e9-867c-4eb4-8bc1-e65e5b3f2aeb
keywords:
- 全局标志实用程序
- 驱动程序验证程序 WDK，全局标志实用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97aefe3397738391d7c510d92aa7028917a2c1b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568775"
---
# <a name="using-the-global-flags-utility"></a>使用全局标志实用工具


## <span id="ddk_using_the_global_flags_utility_tools"></span><span id="DDK_USING_THE_GLOBAL_FLAGS_UTILITY_TOOLS"></span>


全局标志 (gflags.exe) 实用程序提供了在系统注册表中设置某些项、 调整正在运行的系统的内核设置和更改图像文件的设置的简单方法。 可以使用图形化或命令行界面来设置这些项。

Windows 支持工具包在和中的 Windows 调试工具软件包，可找到全局标志实用程序。 有关后者的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

若要配置驱动程序验证程序的特殊池选项，或若要指定在单个内存分配中使用特殊的池，还可以使用全局标志实用程序。

若要更改特殊池设置，请启动全局标志实用工具，并选择**系统注册表**中的选项按钮**目标**部分。 **内核特殊池标记**可以设置某些特殊池选项对话框的部分。

### <a name="span-idcontrollingpooltagalignmentspanspan-idcontrollingpooltagalignmentspancontrolling-pool-tag-alignment"></a><span id="controlling_pool_tag_alignment"></span><span id="CONTROLLING_POOL_TAG_ALIGNMENT"></span>控制池标记对齐方式

选择**验证启动**选项按钮以导致要专注于不足检测的特殊池对齐方式。 选择**验证结束**选项能够专注于溢出检测。 这些按钮是否进行驱动程序验证程序或全局标志控制所有特殊池分配-的对齐的方式。

### <a name="span-idusingspecialpoolbypooltagorallocationsizespanspan-idusingspecialpoolbypooltagorallocationsizespanusing-special-pool-by-pool-tag-or-allocation-size"></a><span id="using_special_pool_by_pool_tag_or_allocation_size"></span><span id="USING_SPECIAL_POOL_BY_POOL_TAG_OR_ALLOCATION_SIZE"></span>使用特殊的池的池标记或分配大小

特殊池可用于所有分配，则使用某些池标记。 若要激活此功能，输入池标记插入**池标记**文本框。

此外可以为某个特定大小范围中的所有分配使用特殊池。 尽管此使用特殊的池不涉及池标记，通过输入数字尽管如此激活此功能**池标记**文本框。 此数字必须小于页面\_大小。

对于 x86 处理器，页\_大小为 0x1000 控制，并且分配大小范围是 8 个字节的长度。 若要激活的所有分配，则在此范围内的大小使用特殊池，请输入一个数等于此范围加上 8 的最大值。 （此数字始终是 8 的倍数。）下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">池标记文本框中输入此号码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 到 8 个字节</p></td>
<td align="left"><p>16 (0x10)</p></td>
</tr>
<tr class="even">
<td align="left"><p>9 到 16 个字节</p></td>
<td align="left"><p>24 (0x18)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>17 到 24 个字节</p></td>
<td align="left"><p>32 (0x20)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFE9 到 0xFF0 字节</p></td>
<td align="left"><p>0xFF8</p></td>
</tr>
</tbody>
</table>

 

对于 x64 处理器，页\_大小为 0x1000 控制，并且分配大小范围是 16 个字节的长度。 若要激活的所有分配，则在此范围内的大小使用特殊池，请输入一个数等于此范围以及 16 的最大值。 （此数字始终是 16 的倍数。）下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">池标记文本框中输入此号码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 到 16 个字节</p></td>
<td align="left"><p>32 (0x20)</p></td>
</tr>
<tr class="even">
<td align="left"><p>17 到 32 个字节</p></td>
<td align="left"><p>48 (0x30)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33 到 48 个字节</p></td>
<td align="left"><p>64 (0x40)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFD1 到 0xFE0 字节</p></td>
<td align="left"><p>0xFF0</p></td>
</tr>
</tbody>
</table>

 

对于基于 Itanium 的处理器，页\_大小是 0x2000 和分配大小范围是 16 个字节的长度。 若要激活的所有分配，则在此范围内的大小使用特殊池，请输入一个数等于此范围以及 16 的最大值。 （此数字始终是 16 的倍数。）下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">池标记文本框中输入此号码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 到 16 个字节</p></td>
<td align="left"><p>32 (0x20)</p></td>
</tr>
<tr class="even">
<td align="left"><p>17 到 32 个字节</p></td>
<td align="left"><p>48 (0x30)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33 到 48 个字节</p></td>
<td align="left"><p>64 (0x40)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1FD1 到 0x1FE0 字节</p></td>
<td align="left"><p>0x1FF0</p></td>
</tr>
</tbody>
</table>

 

最好避免使用低于页池标记\_大小。 例如，如果在基于 Itanium 处理器上将 0x30 放入此文本框中，特殊的池将使用大小，为 17 到 32 个字节之间的所有分配和分配，则使用池标记 0x0030。

**请注意**  特殊池如果驱动程序验证程序已启用驱动程序的特殊池并全局标志实用程序启用了特殊池标记或分配大小的池，将用于满足任何这些条件 （所有分配取决于池可用性）。

 

请参阅[特殊池](special-pool.md)有关使用特殊的池的完整详细信息。

 

 





