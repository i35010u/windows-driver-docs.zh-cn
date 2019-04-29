---
title: 线程语法
description: 线程语法
ms.assetid: f3eaa0ee-7c4f-47a4-aba9-c1d21c1529d1
keywords:
- 线程，命令语法
- ~ （线程标识符）
- 线程的线程标识符 （~）
- 线程，线程 ID
- ~ （线程标识符）
- 语法规则的命令，~ （线程标识符）
- 语法规则的命令，~ （线程标识符）
- 线程的命令的语法规则
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed9b36168fc29b13fbe732662dc4ba2aeea26941
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366099"
---
# <a name="thread-syntax"></a>线程语法


## <span id="ddk_thread_syntax_dbg"></span><span id="DDK_THREAD_SYNTAX_DBG"></span>


许多调试器命令作为其参数具有线程标识符。 波形符 （~） 出现在之前的线程标识符。

线程标识符可以是下列值之一。

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
<td align="left"><p>此进程中的所有线程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>~</strong><em>数量</em></p></td>
<td align="left"><p>其索引的线程<em>数</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>~~</strong>[<em>TID</em>]</p></td>
<td align="left"><p>其线程 ID 是在线程<em>TID</em>。 （括号是必需的和不能添加第二个波形符和左大括号之间有空格）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>~</strong>[<em>表达式</em>]</p></td>
<td align="left"><p>线程的线程 ID 是到整数数值<em>表达式</em>解析。</p></td>
</tr>
</tbody>
</table>

 

线程创建时分配索引。 请注意，此数字与 Microsoft Windows 操作系统使用的线程 ID 不同。

当调试开始时，当前线程是导致出现异常或调试事件 （或活动线程时调试器附加到进程）。 线程保持当前线程，直到指定一个使用的新[ **~ s （设置当前线程）** ](-s--set-current-thread-.md)命令或使用[进程和线程窗口](processes-and-threads-window.md)在 WinDbg 中。

线程标识符通常显示为命令前缀。 请注意，并非所有通配符使用线程标识符的所有命令中提供。

举例说明 ~\[*表达式*\]语法是`~[@$t0]`。 在此示例中，具体取决于用户定义的伪寄存器的值的线程更改。 此语法允许调试器脚本以编程方式选择线程。

### <a name="span-idcontrollingthreadsinkernelmodespanspan-idcontrollingthreadsinkernelmodespancontrolling-threads-in-kernel-mode"></a><span id="controlling_threads_in_kernel_mode"></span><span id="CONTROLLING_THREADS_IN_KERNEL_MODE"></span>在内核模式下控制线程

在内核模式下，不能控制线程，通过使用线程标识符。 有关如何访问在内核模式下的特定于线程的信息的详细信息，请参阅[更改上下文](changing-contexts.md)。

**请注意**  使用波形符 （~） 若要在用户模式下调试过程中指定的线程。 在内核模式调试，可以使用波形符来指定处理器。 有关如何指定处理器的详细信息，请参阅[包含多个处理器语法](multiprocessor-syntax.md)。

 

 

 





