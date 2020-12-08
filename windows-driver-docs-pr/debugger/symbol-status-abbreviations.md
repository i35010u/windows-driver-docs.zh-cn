---
title: 符号状态缩写
description: 符号状态缩写
keywords:
- 符号，符号状态缩写
- '延迟 (符号状态缩写) '
- " (符号状态缩写) "
- 'T (符号状态缩写) '
- 'C (符号状态缩写) '
- 'DIA (符号状态缩写) '
- '导出 (符号状态缩写) '
- 'PERF (符号状态缩写) '
- 'PDB (符号状态缩写) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa5e30526e62ddfaeea4f1558987316a372c0721
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806499"
---
# <a name="symbol-status-abbreviations"></a>符号状态缩写


## <span id="ddk_symbol_status_abbreviations_dbg"></span><span id="DDK_SYMBOL_STATUS_ABBREVIATIONS_DBG"></span>


可以通过使用 " [**lm (列表" 加载的模块)**](lm--list-loaded-modules-.md) 命令、 [**！ Lmi**](-lmi.md) 扩展或 WinDbg 的 "调试" 来确定符号文件类型及其加载状态。 [模块](debug---modules.md) 菜单命令。

其中每个都显示了有关加载的模块及其符号的信息。

以下缩写用于这些命令生成的显示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">缩写</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>延时</strong></p></td>
<td align="left"><p>已加载该模块，但调试器尚未尝试加载这些符号。 需要时将加载符号。 有关详细信息，请参阅 <a href="deferred-symbol-loading.md" data-raw-source="[Deferred Symbol Loading](deferred-symbol-loading.md)">延迟符号加载</a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>符号文件与可执行文件在其时间戳或其校验和中不匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>T</strong></p></td>
<td align="left"><p>时间戳缺失、不可访问或等于零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>C</strong></p></td>
<td align="left"><p>校验和缺失、不可访问或等于零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DIA</strong></p></td>
<td align="left"><p>符号文件是通过调试接口访问 (DIA) 加载的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>导出</strong></p></td>
<td align="left"><p>找不到实际符号文件，因此符号信息是从二进制文件的导出表中提取的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>M</strong></p></td>
<td align="left"><p>符号文件与可执行文件在其时间戳或其校验和中不匹配。 但是，由于符号选项设置，已加载符号文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>性能</strong></p></td>
<td align="left"><p>此二进制文件包含 <a href="debugging-performance-optimized-code.md" data-raw-source="[performance-optimized code](debugging-performance-optimized-code.md)">性能优化的代码</a>。 标准地址算法可能不会生成正确的结果。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>拆卸</strong></p></td>
<td align="left"><p>已从图像文件中去除调试信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>板</strong></p></td>
<td align="left"><p>符号采用 .pdb 格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>COFF</strong></p></td>
<td align="left"><p>符号采用通用对象文件格式 (COFF) 符号格式。</p></td>
</tr>
</tbody>
</table>

 

 

 





