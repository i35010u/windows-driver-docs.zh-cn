---
title: 符号状态缩写
description: 符号状态缩写
ms.assetid: 198453f2-fc9a-4313-875e-ac963b843df9
keywords:
- 符号，符号状态缩写
- 延迟 （符号状态缩写）
- （符号状态缩写）
- T （符号状态缩写）
- C （符号状态缩写）
- DIA （符号状态缩写）
- 导出 （符号状态缩写）
- 性能 （符号状态缩写）
- PDB （符号状态缩写）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7aadee45618c5fddfc3641d2c049b55c719e877
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350358"
---
# <a name="symbol-status-abbreviations"></a>符号状态缩写


## <span id="ddk_symbol_status_abbreviations_dbg"></span><span id="DDK_SYMBOL_STATUS_ABBREVIATIONS_DBG"></span>


可通过使用确定符号的文件类型和它们的加载状态[ **lm （列表加载模块）** ](lm--list-loaded-modules-.md)命令， [ **！ lmi** ](-lmi.md)扩展或 WinDbg 的[调试 |模块](debug---modules.md)菜单命令。

其中每项功能显示有关已加载的模块和其符号的信息。

显示生成的这些命令中使用下列缩写：

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
<td align="left"><p><strong>deferred</strong></p></td>
<td align="left"><p>已加载的模块，但不是调试器尝试加载符号。 在需要时，将加载符号。 请参阅<a href="deferred-symbol-loading.md" data-raw-source="[Deferred Symbol Loading](deferred-symbol-loading.md)">延迟的符号加载</a>有关详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>没有符号文件的可执行文件，其时间戳或其校验和不匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>T</strong></p></td>
<td align="left"><p>时间戳已丢失、 不可访问，或等于零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>C</strong></p></td>
<td align="left"><p>校验和已丢失、 不可访问，或等于零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DIA</strong></p></td>
<td align="left"><p>通过调试接口访问 (DIA) 已加载符号文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Export</strong></p></td>
<td align="left"><p>找到了没有实际符号文件，以便从二进制文件的导出表提取符号信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>M</strong></p></td>
<td align="left"><p>没有符号文件的可执行文件，其时间戳或其校验和不匹配。 但是，符号文件已加载仍要由于符号选项设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>PERF</strong></p></td>
<td align="left"><p>此二进制文件包含<a href="debugging-performance-optimized-code.md" data-raw-source="[performance-optimized code](debugging-performance-optimized-code.md)">性能优化的代码</a>。 标准地址算术可能不会产生正确的结果。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Stripped</strong></p></td>
<td align="left"><p>调试信息已从图像文件中去除。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>PDB</strong></p></td>
<td align="left"><p>符号的.pdb 格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>COFF</strong></p></td>
<td align="left"><p>符号是通用对象文件格式 (COFF) 符号格式。</p></td>
</tr>
</tbody>
</table>

 

 

 





