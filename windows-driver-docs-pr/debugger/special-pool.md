---
title: 特殊的池
description: 特殊的池
ms.assetid: 8904913d-78ed-4e5f-acef-3c21eeb87b8d
keywords:
- 特殊的池
- 特殊的池概述
- GFlags、 特殊的池
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0e21ba07f3506996d5ab113a70b32c6a949c813
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519414"
---
# <a name="special-pool"></a>特殊的池


**特殊池**功能配置 Windows 请求内存分配保留的内存池中时内存分配了指定的池标记或指定的大小范围内。

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
<td align="left"><p>整个系统的注册表项</p>
<p>(Windows Vista 及更高版本)整个系统的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idselectingapooltagspanspan-idselectingapooltagspanselecting-a-pool-tag"></a><span id="selecting_a_pool_tag"></span><span id="SELECTING_A_POOL_TAG"></span>选择池标记

在请求的特定池标记的特殊池时，请确保您的驱动程序或其他内核模式程序使用的唯一池标记。

此外，创建一个池标记时 (如通过使用**ExAllocatePoolWithTag**)，请考虑按相反的顺序输入的标记字符。 例如，如果标记为**Fred**，其作为输入，请考虑**derF** (0x64657246)。 池标记将存储在注册表中，并显示在调试器和反向 （较低字节序） 顺序中的其他工具。 如果按相反的顺序输入它们，它们将显示在正向顺序 (0x46726564)

如果您怀疑您的驱动程序使用所有特殊的池，请考虑在代码中使用多个池标记。 你随后可以测试您的驱动程序多次，将特殊的池分配给每个测试中的一个池标记。

此外，选择具有大于系统页面大小的十六进制值的池标记。 有关内核模式代码，如果输入池标记的值小于页面\_大小，Gflags 请求其大小在相应范围内，并请求特殊池分配，则使用等效的池标记的所有分配的特殊池。 例如，如果您选择的大小**30**，对于大小，为 17 到 32 个字节之间的所有分配和分配，则使用池标记 0x0030，将使用特殊的池。

### <a name="span-idselectinganallocationsizespanspan-idselectinganallocationsizespanselecting-an-allocation-size"></a><span id="selecting_an_allocation_size"></span><span id="SELECTING_AN_ALLOCATION_SIZE"></span>选择分配大小

使用以下准则来选择特殊池功能分配大小。

使用 x86 的计算机上处理器，页\_大小为 0x1000 控制，并且分配大小范围是 8 个字节的长度。 若要配置的大小在此范围内的所有分配的特殊池功能，请输入一个数等于此范围加上 8 的最大值。 （此数字始终是 8 的倍数。）下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">输入此号码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 到 8 个字节</p></td>
<td align="left"><p>10 (十进制 16)</p></td>
</tr>
<tr class="even">
<td align="left"><p>9 到 16 个字节</p></td>
<td align="left"><p>18 (十进制 24)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>17 到 24 个字节</p></td>
<td align="left"><p>20 (十进制 32)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFE9 到 0xFF0 字节</p></td>
<td align="left"><p>FF8 (十进制 4088)</p></td>
</tr>
</tbody>
</table>

 

使用页是 AMD x86-64 处理器的计算机上\_大小为 0x1000 控制，并且分配大小范围是 16 个字节的长度。 若要配置的大小在此范围内的所有分配的特殊池功能，请输入一个数等于此范围以及 16 的最大值。 （此数字始终是 16 的倍数。）下表说明了这些值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小范围</th>
<th align="left">输入此号码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 到 16 个字节</p></td>
<td align="left"><p>20 (十进制 32)</p></td>
</tr>
<tr class="even">
<td align="left"><p>17 到 32 个字节</p></td>
<td align="left"><p>30 （十进制 48 个）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33 到 48 个字节</p></td>
<td align="left"><p>40 (十进制 64)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFD1 到 0xFE0 字节</p></td>
<td align="left"><p>FF0 (十进制 4080)</p></td>
</tr>
</tbody>
</table>

 

在具有任何处理器的计算机，可以使用星号 ( **\\***) 或 0x2A (十进制 42) 若要在系统上配置的所有内存分配的特殊池功能。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

有关在全局标志对话框中配置特殊池功能的信息，请参阅[配置特殊池](configuring-special-pool.md)。 在命令行配置特殊池功能有关的信息，请参阅[ **GFlags 命令**](gflags-commands.md)。 有关示例，请参阅[示例 14:配置特殊池](example-14---configuring-special-pool.md)。

Gflags 的特殊池功能指示 Windows 请求内存分配保留的内存池中时内存分配了指定的池标记或指定的大小范围内。 若要请求的特定驱动程序由特殊池的所有分配，使用驱动程序验证程序。 有关详细信息，请参阅"驱动程序验证程序"部分的 Windows Driver Kit (WDK) 中的"特殊池"主题。

Gflags 和驱动程序验证程序的特殊池功能帮助你检测和识别内核池使用，例如超出了分配的内存空间中，编写或引用已释放的内存中的错误的源。

并非所有特殊池请求完成。 从特殊池中每个分配使用一页的分页物理内存和虚拟地址空间的两个页面。 如果用尽了特殊池，直到再次变为可用的特殊池是从标准池分配内存。 从标准池中填充特殊池请求后发出请求的函数将返回成功状态。 它不返回错误，因为已成功分配，即使它未填充从特殊池也是如此。

特殊的池的大小而增加系统; 上的物理内存量理想情况下，这应至少为 1 千兆字节 (GB)。 在 x86 计算机，因为使用虚拟的 （除了为物理） 空间，不使用**3GB**使用特殊的池时启动选项。 它也是最好的两个或三倍增加页面文件的最小/最大数量。

此外可以配置要对齐内存分配，以检测对前面的分配 （"不足"） 的内存的引用或对超出分配 （"溢出"） 的内存的引用的特殊池功能。 此功能目前仅在所有版本的 Windows 上的全局标志对话框。 有关详细信息，请参阅[检测溢出和不足](detecting-overruns-and-underruns.md)。

在 Windows Vista 和更高版本的 Windows 中，你可以配置特殊池功能，如注册表设置，需要重新启动，但将一直保持有效，直到更改它，或为一个内核标记设置，不需要重新启动，但仅在前您是有效重新启动或关闭 Windows。 在早期版本的 Windows 中，特殊的池才可用的注册表设置。

在 Windows Vista 和更高版本的 Windows 上，可以通过使用全局标志对话框中或在命令行配置特殊池功能。 在早期版本的 Windows 中，此功能目前仅在全局标志对话框中。

 

 





