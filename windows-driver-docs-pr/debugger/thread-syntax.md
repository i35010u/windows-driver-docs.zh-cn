---
title: 线程语法
description: 线程语法
keywords:
- thread、command 语法
- '~ (线程标识符) '
- '线程标识符 ( ~ ) '
- 线程，线程 ID
- '~ (线程标识符) '
- '命令的语法规则 ~ (线程标识符) '
- '命令的语法规则 ~ (线程标识符) '
- 命令、线程的语法规则
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5181521641d7341cb226dc7055dd8ff63e4ce078
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787765"
---
# <a name="thread-syntax"></a>线程语法


## <span id="ddk_thread_syntax_dbg"></span><span id="DDK_THREAD_SYNTAX_DBG"></span>


许多调试器命令都将线程标识符作为其参数。 颚化符 ( ~ ) 出现在线程标识符之前。

线程标识符可以为下列值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">线程标识符</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>~.</strong></p></td>
<td align="left"><p>当前线程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>~#</strong></p></td>
<td align="left"><p>导致当前异常或调试事件的线程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>~*</strong></p></td>
<td align="left"><p>进程中的所有线程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>~</strong><em>多种</em></p></td>
<td align="left"><p>其索引为 <em>数字</em>的线程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>~~</strong>[<em>TID</em>]</p></td>
<td align="left"><p>线程 ID 为 <em>TID</em>的线程。  (括号是必需的，并且不能在第二个波形符和左大括号之间添加空格 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>~</strong>[<em>表达式</em>]</p></td>
<td align="left"><p>线程 ID 为数值 <em>表达式</em> 解析的整数的线程。</p></td>
</tr>
</tbody>
</table>

 

创建线程时，将为其分配索引。 请注意，此数字不同于 Microsoft Windows 操作系统使用的线程 ID。

当调试开始时，当前线程是导致当前异常或调试事件的线程 (或当调试器附加到进程) 时的活动线程。 该线程将保留当前线程，直到你使用 [**~ s (设置当前线程)**](-s--set-current-thread-.md) 命令或使用 WinDbg 中的 " [进程" 和 "线程" 窗口](processes-and-threads-window.md) 指定一个新线程。

线程标识符通常以命令前缀形式出现。 请注意，并不是所有使用线程标识符的命令均提供所有通配符字符。

大约为 ~ \[ *表达式* \] 语法的示例 `~[@$t0]` 。 在此示例中，该线程将根据用户定义的伪寄存器的值发生变化。 此语法允许调试器脚本以编程方式选择一个线程。

### <a name="span-idcontrolling_threads_in_kernel_modespanspan-idcontrolling_threads_in_kernel_modespancontrolling-threads-in-kernel-mode"></a><span id="controlling_threads_in_kernel_mode"></span><span id="CONTROLLING_THREADS_IN_KERNEL_MODE"></span>控制内核模式下的线程

在内核模式下，不能使用线程标识符来控制线程。 有关如何在内核模式下访问线程特定信息的详细信息，请参阅 [更改上下文](changing-contexts.md)。

**注意**  在用户模式调试过程中，可以使用波形符 ( ~ ) 来指定线程。 在内核模式调试中，可以使用波形符来指定处理器。 有关如何指定处理器的详细信息，请参阅 [多处理器语法](multiprocessor-syntax.md)。

 

 

 





