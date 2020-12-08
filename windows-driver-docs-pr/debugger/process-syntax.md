---
title: 进程语法
description: 进程语法
keywords:
- 进程，命令语法
- " (进程标识符) "
- '进程、进程标识符 ( ) '
- '进程 ID (PID) '
- 'PID (进程 ID) '
- " (进程标识符) "
- '命令的语法规则、 (进程标识符) '
- '命令的语法规则、 (进程标识符) '
- '进程标识符 ( ) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 767efced932cfdaccced30d0170b81491a3a9d4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840827"
---
# <a name="process-syntax"></a>进程语法


## <span id="ddk_process_syntax_dbg"></span><span id="DDK_PROCESS_SYNTAX_DBG"></span>


许多调试器命令都将进程标识符作为其参数。 竖线 ( |) 出现在进程标识符之前。

进程标识符可以是下列值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">进程标识符</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>|.</strong></p></td>
<td align="left"><p>当前进程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|#</strong></p></td>
<td align="left"><p>导致当前异常或调试事件的进程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>|*</strong></p></td>
<td align="left"><p>所有进程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|</strong><em>多种</em></p></td>
<td align="left"><p>序数为 <em>Number</em>的进程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>| ~ [</strong><em>PID</em><strong>]</strong></p></td>
<td align="left"><p>进程 ID 为 <em>PID</em>的进程。  (括号是必需的，并且不能在波形符 (~) 和左括号之间添加空格。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|[</strong><em>表达式</em><strong>]</strong></p></td>
<td align="left"><p>其进程 ID 为数值 <em>表达式</em> 解析的整数的进程。</p></td>
</tr>
</tbody>
</table>

 

创建进程时，将为其分配序号。 请注意，此数字不同于 Microsoft Windows 操作系统使用的进程 ID (PID) 。

当前过程定义了所使用的内存空间和线程集。 调试开始时，当前进程是导致当前异常或调试事件 (或调试器附加到) 的进程。 该进程将保持当前进程，直到你使用 [**| s (设置当前进程)**](-s--set-current-process-.md) 命令或使用 WinDbg 中的 " [进程和线程" 窗口](processes-and-threads-window.md) 指定新进程。

进程标识符在多个命令中用作参数，通常作为命令前缀。 请注意，WinDbg 和 CDB 可以调试原始进程创建的子进程。 WinDbg 和 CDB 还可以附加到多个无关的进程。

| \[ 的示例 *表达式* \]语法为 | \[@ $t 0 \] 。 在此示例中，该过程将根据用户定义的伪寄存器的值发生变化。 此语法允许调试器脚本以编程方式选择进程。

### <a name="span-idcontrolling_processes_in_kernel_modespanspan-idcontrolling_processes_in_kernel_modespancontrolling-processes-in-kernel-mode"></a><span id="controlling_processes_in_kernel_mode"></span><span id="CONTROLLING_PROCESSES_IN_KERNEL_MODE"></span>控制内核模式下的进程

在内核模式下，不能使用进程标识符来控制进程。 有关如何访问内核模式下特定于进程的信息的详细信息，请参阅 [更改上下文](changing-contexts.md)。

 

 





