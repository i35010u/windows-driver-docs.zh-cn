---
title: 过程语法
description: 过程语法
ms.assetid: fe08b5fe-ec27-4264-baee-de4c11bcb2bf
keywords:
- 过程中，命令语法
- （进程标识符）
- 过程中，进程标识符 （）
- 进程的进程 ID (PID)
- PID (进程 ID)
- （进程标识符）
- （进程标识符） 的命令的语法规则
- （进程标识符） 的命令的语法规则
- 进程标识符 （)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e300706debbbbfae9bc08aa15acef5c07e8c0412
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526823"
---
# <a name="process-syntax"></a>过程语法


## <span id="ddk_process_syntax_dbg"></span><span id="DDK_PROCESS_SYNTAX_DBG"></span>


许多调试器命令作为其参数具有进程标识符。 垂直条 (|) 出现在之前的进程标识符。

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
<td align="left"><p>引起当前异常或调试事件的进程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>|*</strong></p></td>
<td align="left"><p>所有进程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|</strong><em>数量</em></p></td>
<td align="left"><p>进程的第几<em>数</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>|~[</strong><em>PID</em><strong>]</strong></p></td>
<td align="left"><p>进程的进程 ID <em>PID</em>。 （括号是必需的和不能添加颚化符 （~） 和左大括号之间有空格）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|[</strong><em>Expression</em><strong>]</strong></p></td>
<td align="left"><p>其进程 ID 的整数进程数值<em>表达式</em>解析。</p></td>
</tr>
</tbody>
</table>

 

创建进程分配序号。 请注意，此数字与进程 ID (PID) 的 Microsoft Windows 操作系统使用不同。

当前进程定义的内存空间和使用的线程的集。 当调试开始时，当前进程是导致出现异常或调试事件 （或调试器附加到进程）。 进程保持当前进程，直到指定一个使用的新[ **| s （设置当前进程）** ](-s--set-current-process-.md)命令或使用[进程和线程窗口](processes-and-threads-window.md)在 WinDbg 中.

进程标识符作为参数在多个命令中，经常使用作为命令前缀。 请注意 WinDbg 和 CDB 可以调试原始进程创建的子进程。 WinDbg 和 CDB 还可以附加到多个不相关的进程。

举例说明 |\[*表达式*\]语法是\[|@$t0\]。 在此示例中，具体取决于用户定义的伪寄存器的值更改过程。 此语法允许调试器脚本以编程方式选择的进程。

### <a name="span-idcontrollingprocessesinkernelmodespanspan-idcontrollingprocessesinkernelmodespancontrolling-processes-in-kernel-mode"></a><span id="controlling_processes_in_kernel_mode"></span><span id="CONTROLLING_PROCESSES_IN_KERNEL_MODE"></span>控制在内核模式下的进程

在内核模式下，不能使用进程标识符来控制进程。 有关如何访问在内核模式下的特定于进程的信息的详细信息，请参阅[更改上下文](changing-contexts.md)。

 

 





