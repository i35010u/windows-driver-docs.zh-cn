---
title: 特殊池
description: 特殊池
keywords:
- 特殊池
- 特殊池，概述
- GFlags，特殊池
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b1135e670f0c1ede48e4e21f16f7299b4377345
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791643"
---
# <a name="special-pool"></a>特殊池


**特殊池** 功能可将 Windows 配置为在使用指定的池标记分配内存或在指定大小范围内时，请求保留内存池中的内存分配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>spp</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>（无）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>（无）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项</p>
<p> (Windows Vista 及更高版本) 系统范围内的注册表项、内核标志</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idselecting_a_pool_tagspanspan-idselecting_a_pool_tagspanselecting-a-pool-tag"></a><span id="selecting_a_pool_tag"></span><span id="SELECTING_A_POOL_TAG"></span>选择池标记

请求特定池标记的特殊池时，请确保你的驱动程序或其他内核模式程序使用唯一的池标记。

另外，在创建池标记 (例如使用 **ExAllocatePoolWithTag**) 时，请考虑按相反的顺序输入标记字符。 例如，如果标记是 **Fred** 标记，请考虑将其输入为 **derF** (0x64657246) 。 池标记存储在注册表中，并以反向顺序显示在调试器和其他工具中 (以较低的字节序) 顺序。 如果按相反的顺序输入，则它们将按正向顺序显示 (0x46726564) 

如果您怀疑您的驱动程序正在使用所有特殊池，请考虑在您的代码中使用多个池标记。 然后，可以多次测试您的驱动程序，并在每个测试中为一个池标记分配特殊的池。

另外，请选择一个具有大于系统页面大小的十六进制值的池标记。 对于内核模式代码，如果输入的池标记的值小于页面 \_ 大小，则 Gflags 会为大小在相应范围内的所有分配请求特殊池，并请求具有等效池标记的分配的特殊池。 例如，如果选择的大小为 **30**，则会将特殊池用于大小介于17到32字节之间的所有分配，并用于使用池标记0x0030 的分配。

### <a name="span-idselecting_an_allocation_sizespanspan-idselecting_an_allocation_sizespanselecting-an-allocation-size"></a><span id="selecting_an_allocation_size"></span><span id="SELECTING_AN_ALLOCATION_SIZE"></span>选择分配大小

使用以下准则来为特殊池功能选择分配大小。

在具有 x86 处理器的计算机上，页 \_ 大小为0x1000，分配大小范围为8个字节。 若要为此范围内所有大小的分配配置特殊池功能，请输入一个等于此范围的最大值加上8的数字。  (此数字始终为8的倍数。 ) 下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">输入此编号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1到8个字节</p></td>
<td align="left"><p>10 (十进制 16) </p></td>
</tr>
<tr class="even">
<td align="left"><p>9到16字节</p></td>
<td align="left"><p>18 (decimal 24) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>17到24字节</p></td>
<td align="left"><p>20 (十进制 32) </p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFE9 to 0xFF0 bytes</p></td>
<td align="left"><p>FF8 (十进制 4088) </p></td>
</tr>
</tbody>
</table>

 

在具有 AMD x86-64 处理器的计算机上，页 \_ 大小为0x1000，分配大小范围是16个字节。 若要为大小在此范围内的所有分配配置特殊池功能，请输入一个等于此范围的最大值加16的数字。  (此数字始终为16的倍数。 ) 下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">输入此编号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1到16字节</p></td>
<td align="left"><p>20 (十进制 32) </p></td>
</tr>
<tr class="even">
<td align="left"><p>17到32字节</p></td>
<td align="left"><p>30 (十进制 48) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>33到48字节</p></td>
<td align="left"><p>40 (十进制 64) </p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFD1 to 0xFE0 bytes</p></td>
<td align="left"><p>FF0 (十进制 4080) </p></td>
</tr>
</tbody>
</table>

 

在具有任何处理器的计算机上，可以使用星号 ( * *\** _ ) 或 0x2A (decimal 42) 为系统上的所有内存分配配置特殊池功能。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

有关在 "全局标志" 对话框中配置 "特殊池" 功能的信息，请参阅 [配置特殊池](configuring-special-pool.md)。 有关在命令行配置特殊池功能的信息，请参阅 [_ *GFlags 命令* *](gflags-commands.md)。 有关示例，请参阅 [示例14：配置特殊池](example-14---configuring-special-pool.md)。

当使用指定的池标记分配内存或在指定的大小范围内时，Gflags 的特殊池功能指导 Windows 请求从保留内存池中分配内存。 若要为特定驱动程序请求所有分配的特殊池，请使用驱动程序验证程序。 有关详细信息，请参阅 Windows 驱动程序工具包 (WDK) 的 "驱动程序验证程序" 部分中的 "特殊池" 主题。

Gflags 和 Driver Verifier 的特殊池功能可帮助检测和确定内核池使用中的错误源，如写入超出分配的内存空间，或引用已释放的内存。

并非所有特殊的池请求均已完成。 每个来自特殊池的分配都使用一页不可分页物理内存和两页虚拟地址空间。 如果特殊池用尽，则会从标准池中分配内存，直到该专用池再次变为可用。 当从标准池中填充特殊的池请求时，请求函数将返回成功状态。 它不会返回错误，因为分配已成功，即使它未从特殊池填充。

特殊池的大小增加了系统上的物理内存量;理想情况下，应至少为1千兆字节 (GB) 。 在 x86 计算机上，由于虚拟 (除了使用物理) 空间以外，在使用特殊池时，请不要使用 **/3gb** boot 选项。 最好是将页面文件的最小/最大数量提高一倍。

你还可以配置 "特殊池" 功能，以便在分配 ( "不足 ) " 之前检测对内存的引用并检测对超出分配 ( "溢出" ) 内存的引用。 此功能仅在所有版本的 Windows 上的 "全局标志" 对话框中可用。 有关详细信息，请参阅 [检测超支和不足](detecting-overruns-and-underruns.md)。

在 Windows Vista 和更高版本的 Windows 上，你可以将特殊池功能配置为需要重新启动的注册表设置，但在更改它之前保持有效，或者作为不需要重新启动的内核标志设置，但仅在重启或关闭 Windows 之前有效。 在较早版本的 Windows 中，特殊池只能用作注册表设置。

在 Windows Vista 和更高版本的 Windows 上，可以使用 "全局标志" 对话框或命令行来配置特殊的池功能。 在早期版本的 Windows 中，此功能仅在 "全局标志" 对话框中可用。

 

 





