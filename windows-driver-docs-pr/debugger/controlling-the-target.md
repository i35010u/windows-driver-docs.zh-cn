---
title: 控制目标
description: 控制目标
keywords:
- 控制目标
- 控制目标，概述
- 启动和停止目标
- 目标的执行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5613f8b385c69230d932bb188755c5b1051cac4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833719"
---
# <a name="controlling-the-target"></a>控制目标


## <span id="ddk_controlling_the_target_dbg"></span><span id="DDK_CONTROLLING_THE_TARGET_DBG"></span>


在用户模式下调试目标应用程序时，或在内核模式下调试目标计算机时，目标可以是 *正在运行* 或 *已停止*。

当调试器连接到内核模式目标时，调试器会使目标保持运行状态，除非使用 **-b** [命令行选项](command-line-options.md)，否则目标系统已停止响应 (即， *崩溃*) ，或由于先前的内核调试操作而导致目标系统仍处于停止状态。

调试器启动或连接到用户模式目标时，调试器会立即停止目标，除非使用 **-g** 命令行选项。 有关详细信息，请参阅 [初始断点](initial-breakpoint.md)。

### <a name="span-idwhen_the_target_is_runningspanspan-idwhen_the_target_is_runningspanwhen-the-target-is-running"></a><span id="when_the_target_is_running"></span><span id="WHEN_THE_TARGET_IS_RUNNING"></span>当目标正在运行时

当目标正在运行时，大多数调试器操作都不可用。

如果要停止正在运行的目标，可以发出 **Break** 命令。 此命令会使调试器 *中断目标*。 也就是说，调试器停止目标，并向调试器提供所有控件。 应用程序可能不会立即中断。 例如，如果所有线程当前正在执行系统代码，或处于等待操作，则应用程序仅在控件返回到应用程序的代码后中断。

如果正在运行的目标遇到异常，则在发生某些 [事件](controlling-exceptions-and-events.md) 时，如果命中 [断点](using-breakpoints.md) ，或者如果应用程序正常关闭，则目标 *中断调试器*。 此操作将停止目标并为调试器提供所有控制权。 调试器中会出现一条消息 [命令窗口](debugger-command-window.md) ，并介绍错误、事件或断点。

### <a name="span-idwhen_the_target_is_stoppedspanspan-idwhen_the_target_is_stoppedspanwhen-the-target-is-stopped"></a><span id="when_the_target_is_stopped"></span><span id="WHEN_THE_TARGET_IS_STOPPED"></span>目标停止时

若要启动或控制目标的执行，可以执行以下操作：

-   若要使应用程序开始运行，请发出 " **开始** " 命令。

-   若要单步执行应用程序一次，请使用 " **逐** 过程" 或 " **逐过程执行** " 命令。 如果发生函数调用，则 **单步** 执行进入函数并继续单步执行每个指令。 "**逐过程**" 将函数调用视为单个步骤。 调试器处于 [程序集模式](debugging-in-assembly-mode.md)时，单步执行一次一次计算机指令。 调试器处于 [源模式](debugging-in-source-mode.md)时，单步执行一次一个源行。

-   若要完成当前函数并在返回发生时停止，请使用 **跳出** 或 **Trace 和 Watch** 命令。 " **跳出** " 命令将继续，直到当前函数结束。 **跟踪和监视** 将继续，直到当前函数结束，并显示函数调用的摘要。 但是，必须在相关函数的第一个指令上发出 **跟踪和监视** 命令。

-   如果发生异常，则可以使用 " **处理异常** 并继续" 和 " **异常未处理** " 命令继续执行并控制异常状态。  (有关异常的详细信息，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。 ) 

-    (WinDbg 仅) 如果在 " [反汇编" 窗口](disassembly-window.md) 或 [源窗口](source-window.md) 中选择某行，然后使用 " **运行到光标处** " 命令，则程序将一直运行，直到它遇到所选的行。

-    (用户模式仅) 关闭目标应用程序并从头开始重新启动该应用程序，请使用 " **重新启动** " 命令。 只能将此命令用于调试器创建的进程。 进程重新启动后，它会立即中断到调试器。

-    (WinDbg 仅) 关闭目标应用程序并清除调试器，请使用 " **停止调试** " 命令。 使用此命令可以开始调试其他目标。

### <a name="span-idcommand_formsspanspan-idcommand_formsspancommand-forms"></a><span id="command_forms"></span><span id="COMMAND_FORMS"></span>命令窗体

用于启动或控制目标执行的大多数命令作为文本命令、菜单命令、工具栏按钮和快捷键存在。 作为基本的文本命令，你可以在 CDB、KD 或 WinDbg 中使用这些命令。  (命令的文本形式通常支持其他选项，例如更改程序计数器的位置或执行固定数目的指令。 ) 可以在 WinDbg 中使用菜单命令、工具栏按钮和快捷键。

您可以使用以下形式的命令。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">WinDbg 按钮</th>
<th align="left">WinDbg 命令</th>
<th align="left">WinDbg 快捷键</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><img src="images/tbcursor.png" alt="Screen shot of the Run to Cursor button" /></td>
<td align="left"><p><a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">调试 | 运行到光标处</a></p></td>
<td align="left"><p>F7</p>
<p>CTRL + F10</p></td>
<td align="left"><p> (WinDbg 仅) 执行，直到到达光标标记的行。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><img src="images/tbstop.png" alt="Screen shot of the Stop Debugging button" /></td>
<td align="left"><p><a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">调试 | 停止调试</a></p></td>
<td align="left"><p>SHIFT + F5</p></td>
<td align="left"><p>停止所有调试并关闭目标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p> (CDB/KD 仅) <strong> <a href="ctrl-c--break-.md" data-raw-source="[CTRL+C](ctrl-c--break-.md)">CTRL + C</a></strong></p></td>
<td align="left"><img src="images/tbbreak.png" alt="Screen shot of the Break button" /></td>
<td align="left"><p><a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">调试 | 中断</a></p></td>
<td align="left"><p>CTRL + BREAK</p></td>
<td align="left"><p>执行将停止，并且调试器将进入目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-restart--restart-target-application-.md" data-raw-source="[.restart (Restart Target Application)](-restart--restart-target-application-.md)">.restart（重启目标应用程序）</a></strong></p></td>
<td align="left"><img src="images/tbrestart.png" alt="Screen shot of the Restart button" /></td>
<td align="left"><p><a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">调试 | 重启</a></p></td>
<td align="left"><p>CTRL + SHIFT + F5</p></td>
<td align="left"><p>仅) 重新启动目标应用程序 (用户模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="g--go-.md" data-raw-source="[g (Go)](g--go-.md)">g（转到）</a></strong></p></td>
<td align="left"><img src="images/tbgo.png" alt="Screen shot of the Go button" /></td>
<td align="left"><p><a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">调试 | 转到</a></p></td>
<td align="left"><p>F5</p></td>
<td align="left"><p>目标任意执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="gc--go-from-conditional-breakpoint-.md" data-raw-source="[gc (Go from Conditional Breakpoint)](gc--go-from-conditional-breakpoint-.md)">gc（从条件断点继续）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>在 <a href="setting-a-conditional-breakpoint.md" data-raw-source="[conditional breakpoint](setting-a-conditional-breakpoint.md)">条件断点</a>之后继续执行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="gh--go-with-exception-handled-.md" data-raw-source="[gh (Go with Exception Handled)](gh--go-with-exception-handled-.md)">gh（转到已处理的异常）</a></strong></p></td>
<td align="left"></td>
<td align="left"><p><a href="debug---go-handled-exception.md" data-raw-source="[Debug | Go Handled Exception](debug---go-handled-exception.md)">调试 | 转到已处理的异常</a></p></td>
<td align="left"></td>
<td align="left"><p>与 <strong>g (中转) </strong>相同，不同之处在于当前异常被视为已处理。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="gn--gn--go-with-exception-not-handled-.md" data-raw-source="[gn (Go with Exception Not Handled)](gn--gn--go-with-exception-not-handled-.md)">gn (不处理异常) </a></strong></p></td>
<td align="left"></td>
<td align="left"><p><a href="debug---go-unhandled-exception.md" data-raw-source="[Debug | Go Unhandled Exception](debug---go-unhandled-exception.md)">调试 | 转到未经处理的异常</a></p></td>
<td align="left"></td>
<td align="left"><p>与 <strong>g (中转) </strong>相同，只不过当前异常被视为未处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="gu--go-up-.md" data-raw-source="[gu (Go Up)](gu--go-up-.md)">gu（向上）</a></strong></p></td>
<td align="left"><img src="images/tbout.png" alt="Screen shot of the Step Out button" /></td>
<td align="left"><p><a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">调试 | 跳出</a></p></td>
<td align="left"><p>SHIFT + F11</p></td>
<td align="left"><p>目标执行到当前函数完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="p--step-.md" data-raw-source="[p (Step)](p--step-.md)">p（步进）</a></strong></p></td>
<td align="left"><img src="images/tbover.png" alt="Screen shot of the Step Over button" /></td>
<td align="left"><p><a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">调试 | 逐步运行</a></p></td>
<td align="left"><p>F10</p></td>
<td align="left"><p>目标执行一条指令。 如果此指令为函数调用，则该函数将作为单个步骤执行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pa--step-to-address-.md" data-raw-source="[pa (Step to Address)](pa--step-to-address-.md)">pa（步进到地址）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标在到达指定地址之前执行。 此函数中的所有步骤都 (显示，但不) 调用的函数中的步骤。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="pc--step-to-next-call-.md" data-raw-source="[pc (Step to Next Call)](pc--step-to-next-call-.md)">pc（步进到下一个调用）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标将在下一次 <strong>调用</strong> 指令之前执行。 如果当前指令是 <strong>调用</strong> 指令，则此调用将被完全执行，执行将继续，直到下一次 <strong>调用</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pct--step-to-next-call-or-return-.md" data-raw-source="[pct (Step to Next Call or Return)](pct--step-to-next-call-or-return-.md)">pct（步进到下一个 Call 或 Return）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标在到达 <strong>调用</strong> 指令或 <strong>返回</strong> 指令之前执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="ph--step-to-next-branching-instruction-.md" data-raw-source="[ph (Step to Next Branching Instruction)](ph--step-to-next-branching-instruction-.md)">ph（步进到下一个分支指令）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行到任何类型的分支指令，包括条件或无条件分支、调用、返回和系统调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pt--step-to-next-return-.md" data-raw-source="[pt (Step to Next Return)](pt--step-to-next-return-.md)">pt（步进到下一个 Return）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标在到达 <strong>返回</strong> 指令之前执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="t--trace-.md" data-raw-source="[t (Trace)](t--trace-.md)">t（跟踪）</a></strong></p></td>
<td align="left"><img src="images/tbinto.png" alt="Screen shot of the Step Into button" /></td>
<td align="left"><p><a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">调试 | 跳入</a></p></td>
<td align="left"><p>F11</p>
<p>F8</p></td>
<td align="left"><p>目标执行一条指令。 如果此指令为函数调用，调试器将跟踪该调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="ta--trace-to-address-.md" data-raw-source="[ta (Trace to Address)](ta--trace-to-address-.md)">ta（跟踪到地址）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标在到达指定地址之前执行。 将显示此函数中的所有步骤和被调用函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tb--trace-to-next-branch-.md" data-raw-source="[tb (Trace to Next Branch)](tb--trace-to-next-branch-.md)">tb（跟踪到下一个分支）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p> (除内核模式之外的所有模式，只有在基于 x86 的系统上，才能执行) 目标，直到到达下一个分支指令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="tc--trace-to-next-call-.md" data-raw-source="[tc (Trace to Next Call)](tc--trace-to-next-call-.md)">tc（跟踪到下一个调用）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标将在下一次 <strong>调用</strong> 指令之前执行。 如果当前指令是 <strong>调用</strong> 指令，则在到达新的 <strong>调用</strong> 之前跟踪指令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tct--trace-to-next-call-or-return-.md" data-raw-source="[tct (Trace to Next Call or Return)](tct--trace-to-next-call-or-return-.md)">tct（跟踪到下一个 Call 或 Return）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标一直执行，直到到达 <strong>call</strong> 指令或 <strong>返回</strong> 指令。 如果当前指令是 <strong>调用</strong> 指令或 <strong>返回</strong> 指令，则在到达新的 <strong>调用</strong> 或 <strong>返回</strong> 之前，将跟踪指令到中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="th--trace-to-next-branching-instruction-.md" data-raw-source="[th (Trace to Next Branching Instruction)](th--trace-to-next-branching-instruction-.md)">th（跟踪到下一个分支指令）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行到任何类型的分支指令，包括条件或无条件分支、调用、返回和系统调用。 如果当前指令是分支指令，则在到达新的分支指令之前跟踪指令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tt--trace-to-next-return-.md" data-raw-source="[tt (Trace to Next Return)](tt--trace-to-next-return-.md)">tt（跟踪到下一个 Return）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标在到达 <strong>返回</strong> 指令之前执行。 如果当前指令是 <strong>返回</strong> 指令，则在到达新的 <strong>返回</strong> 之前跟踪指令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="wt--trace-and-watch-data-.md" data-raw-source="[wt (Trace and Watch Data)](wt--trace-and-watch-data-.md)">wt（跟踪和监视数据）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标在整个指定函数完成之前执行。 随后会显示统计信息。</p></td>
</tr>
</tbody>
</table>

 

有关如何重启目标计算机的详细信息，请参阅 [崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

### <a name="span-idcommand_line_optionsspanspan-idcommand_line_optionsspancommand-line-options"></a><span id="command_line_options"></span><span id="COMMAND_LINE_OPTIONS"></span>命令行选项

如果你不希望应用程序在启动或加载时立即停止，请将 CDB 或 WinDbg 与 **-g** 命令行选项一起使用。 有关此情况的详细信息，请参阅 [初始断点](initial-breakpoint.md)。

CDB 和 WinDbg 还支持 **-G** [命令行选项](command-line-options.md)。 如果应用程序正确完成，则此选项将导致调试会话结束。

下面的命令尝试从开始到完成运行应用程序，并且仅当发生错误时，才会显示调试器提示。

```console
cdb -g -G ApplicationName 
```

可以使用 **-pt** [命令行选项](command-line-options.md) 来设置中断超时。有些问题可能会使目标无法与调试器通信。 如果发出 break 命令并且调试器不能在此时间后进入目标，则调试器会显示 "中断超时" 消息。

此时，调试器将停止尝试进入目标。 相反，调试器会暂停目标，并使您能够检查 (但不能控制目标应用程序) 。

默认超时值为30秒。

 

 





