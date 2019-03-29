---
title: 控制目标
description: 控制目标
ms.assetid: bc08b925-2a55-4af6-a5e2-949637a4c7ee
keywords:
- 控制目标
- 控制目标，概述
- 启动和停止目标
- 目标执行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2acf1e476f88b61b83056ae1a3340264d78909f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562555"
---
# <a name="controlling-the-target"></a>控制目标


## <span id="ddk_controlling_the_target_dbg"></span><span id="DDK_CONTROLLING_THE_TARGET_DBG"></span>


当调试目标应用程序在用户模式下或在内核模式下的目标计算机时，目标可以是*运行*或*停止*。

当调试器连接到内核模式目标时，调试器离开目标运行，除非使用 **-b** [命令行选项](command-line-options.md)，目标系统已停止响应 (即*崩溃*)，或在目标系统仍由于早期的内核调试操作而停止。

当调试器启动或连接到用户模式目标时，调试器立即停止目标，除非使用 **-g**命令行选项。 有关详细信息，请参阅[初始断点](initial-breakpoint.md)。

### <a name="span-idwhenthetargetisrunningspanspan-idwhenthetargetisrunningspanwhen-the-target-is-running"></a><span id="when_the_target_is_running"></span><span id="WHEN_THE_TARGET_IS_RUNNING"></span>目标运行时

目标运行时，大多数调试器操作不可用。

如果你想要停止正在运行的目标，可以发出**中断**命令。 此命令将导致到调试器*分解为目标*。 也就是说，调试器将停止目标和所有控制权都交给调试器。 应用程序可能不会立即中断。 例如，如果所有线程当前正在执行系统代码，或在等待操作中，仅后控件已返回到应用程序的代码将中断该应用程序。

如果正在运行的目标时遇到异常，如果某些[事件](controlling-exceptions-and-events.md)出现，如果[断点](using-breakpoints.md)到达时，或如果在应用程序通常情况下，关闭目标*进入调试器*. 此操作将停止目标，并将所有控制权交给调试器。 在出现一条消息[调试器命令窗口](debugger-command-window.md)并描述了错误、 事件或断点。

### <a name="span-idwhenthetargetisstoppedspanspan-idwhenthetargetisstoppedspanwhen-the-target-is-stopped"></a><span id="when_the_target_is_stopped"></span><span id="WHEN_THE_TARGET_IS_STOPPED"></span>目标的停止时间

若要开始或控制目标的执行，请执行以下操作：

-   若要使应用程序开始运行，发出**转**命令。

-   若要单步执行一次的应用程序一个指令，使用**单步执行**或**单步跳过**命令。 如果函数调用发生，**单步执行**进入函数并继续单步执行通过每个指令。 **单步跳过**视为单步执行函数调用。 当在调试器处于[程序集模式](debugging-in-assembly-mode.md)，单步执行发生一次一个机器指令。 当在调试器处于[源模式](debugging-in-source-mode.md)，单步执行一次发生一个源行。

-   若要完成的当前函数和停止返回发生时，使用**单步跳出**或**跟踪和监视**命令。 **单步跳出**当前函数结束之前，命令会继续运行。 **跟踪和监视**将继续，直到当前函数结束，并且还显示函数的调用的摘要。 但是，必须发出**跟踪和监视**命令相关的函数的第一个指令。

-   如果发生异常，则可以使用**与异常处理**并**与未处理异常**命令继续执行并控制异常的状态。 (有关异常的详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。)

-   (仅 WinDbg)如果选择中的行[反汇编窗口](disassembly-window.md)或[源窗口](source-window.md)，然后使用**运行到光标处**命令时，该程序运行，直到它遇到所选的行。

-   （仅限用户模式）若要关闭目标应用程序，并从开始处重新启动它，请使用**重新启动**命令。 仅与调试器创建的过程，可以使用此命令。 该进程重新启动后，它将立即进入调试器。

-   (仅 WinDbg)若要关闭目标应用程序，并清除调试器，请使用**停止调试**命令。 此命令，可开始调试一个不同的目标。

### <a name="span-idcommandformsspanspan-idcommandformsspancommand-forms"></a><span id="command_forms"></span><span id="COMMAND_FORMS"></span>命令窗体

用于启动或控制的目标执行的大多数命令存在作为文本命令、 菜单命令、 工具栏按钮和键盘快捷方式。 作为基本的文本命令，可以使用这些命令的 CDB、 KD 或 WinDbg。 （文本格式的命令通常支持其他选项，如更改的程序计数器位置或执行固定的数量的说明。）在 WinDbg 中，可以使用菜单命令、 工具栏按钮和键盘快捷方式。

可以在以下窗体中使用命令。

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
<th align="left">Command</th>
<th align="left">WinDbg 按钮</th>
<th align="left">WinDbg 命令</th>
<th align="left">WinDbg 键盘快捷方式</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><img src="images/tbcursor.png" alt="Screen shot of the Run to Cursor button" /></td>
<td align="left"><p><a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">调试 |运行到光标处</a></p></td>
<td align="left"><p>F7</p>
<p>CTRL + F10</p></td>
<td align="left"><p>(仅 WinDbg)执行，直到其达到光标将标记的行。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><img src="images/tbstop.png" alt="Screen shot of the Stop Debugging button" /></td>
<td align="left"><p><a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">调试 |停止调试</a></p></td>
<td align="left"><p>SHIFT + F5</p></td>
<td align="left"><p>停止所有调试并关闭目标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>(仅 CDB/KD) <strong><a href="ctrl-c--break-.md" data-raw-source="[CTRL+C](ctrl-c--break-.md)">CTRL + C</a></strong></p></td>
<td align="left"><img src="images/tbbreak.png" alt="Screen shot of the Break button" /></td>
<td align="left"><p><a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">调试 |中断</a></p></td>
<td align="left"><p>CTRL + BREAK</p></td>
<td align="left"><p>执行将停止，并对目标调试器中断。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-restart--restart-target-application-.md" data-raw-source="[.restart (Restart Target Application)](-restart--restart-target-application-.md)">.restart （重新启动目标应用程序）</a></strong></p></td>
<td align="left"><img src="images/tbrestart.png" alt="Screen shot of the Restart button" /></td>
<td align="left"><p><a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">调试 |重新启动</a></p></td>
<td align="left"><p>CTRL + SHIFT + F5</p></td>
<td align="left"><p>（仅限用户模式）重新启动目标应用程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="g--go-.md" data-raw-source="[g (Go)](g--go-.md)">g （转向）</a></strong></p></td>
<td align="left"><img src="images/tbgo.png" alt="Screen shot of the Go button" /></td>
<td align="left"><p><a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">调试 |转到</a></p></td>
<td align="left"><p>F5</p></td>
<td align="left"><p>目标自由地执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="gc--go-from-conditional-breakpoint-.md" data-raw-source="[gc (Go from Conditional Breakpoint)](gc--go-from-conditional-breakpoint-.md)">gc （从条件性断点转）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>恢复后的执行<a href="setting-a-conditional-breakpoint.md" data-raw-source="[conditional breakpoint](setting-a-conditional-breakpoint.md)">条件断点</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="gh--go-with-exception-handled-.md" data-raw-source="[gh (Go with Exception Handled)](gh--go-with-exception-handled-.md)">gh （转到异常处理）</a></strong></p></td>
<td align="left"></td>
<td align="left"><p><a href="debug---go-handled-exception.md" data-raw-source="[Debug | Go Handled Exception](debug---go-handled-exception.md)">调试 |转到处理异常</a></p></td>
<td align="left"></td>
<td align="left"><p>与相同<strong>g （转向）</strong>，不同之处在于当前异常被视为处理。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="gn--gn--go-with-exception-not-handled-.md" data-raw-source="[gn (Go with Exception Not Handled)](gn--gn--go-with-exception-not-handled-.md)">gn (Go 出现未处理的异常)</a></strong></p></td>
<td align="left"></td>
<td align="left"><p><a href="debug---go-unhandled-exception.md" data-raw-source="[Debug | Go Unhandled Exception](debug---go-unhandled-exception.md)">调试 |转到未经处理的异常</a></p></td>
<td align="left"></td>
<td align="left"><p>与相同<strong>g （转向）</strong>，不同之处在于处理当前异常，未处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="gu--go-up-.md" data-raw-source="[gu (Go Up)](gu--go-up-.md)">gu （向上转）</a></strong></p></td>
<td align="left"><img src="images/tbout.png" alt="Screen shot of the Step Out button" /></td>
<td align="left"><p><a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">调试 |跳出</a></p></td>
<td align="left"><p>SHIFT + F11</p></td>
<td align="left"><p>目标执行，直到当前函数已完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="p--step-.md" data-raw-source="[p (Step)](p--step-.md)">p （步骤）</a></strong></p></td>
<td align="left"><img src="images/tbover.png" alt="Screen shot of the Step Over button" /></td>
<td align="left"><p><a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">调试 |逐过程执行</a></p></td>
<td align="left"><p>F10</p></td>
<td align="left"><p>目标执行一条指令。 如果此指令的函数调用，该函数将作为一个步骤执行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pa--step-to-address-.md" data-raw-source="[pa (Step to Address)](pa--step-to-address-.md)">pa （到地址的步骤）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行，直到它达到指定的地址。 显示此函数中的所有步骤 （但不执行步骤中调用的函数）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="pc--step-to-next-call-.md" data-raw-source="[pc (Step to Next Call)](pc--step-to-next-call-.md)">pc （到下一次调用步骤）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>直到出现下一个执行目标<strong>调用</strong>指令。 如果当前指令<strong>调用</strong>指令，完全执行此调用，并执行将继续，直到下一步<strong>调用</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pct--step-to-next-call-or-return-.md" data-raw-source="[pct (Step to Next Call or Return)](pct--step-to-next-call-or-return-.md)">pct （下一步调用或返回到步骤）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行，直到它达到<strong>调用</strong>指令或<strong>返回</strong>指令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="ph--step-to-next-branching-instruction-.md" data-raw-source="[ph (Step to Next Branching Instruction)](ph--step-to-next-branching-instruction-.md)">p h （到下一个分支指令的步骤）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行，直到它达到包括条件分支指令的任何类型或无条件分支，调用返回，并且系统调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="pt--step-to-next-return-.md" data-raw-source="[pt (Step to Next Return)](pt--step-to-next-return-.md)">pt （到下一步返回的步骤）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行，直到它达到<strong>返回</strong>指令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="t--trace-.md" data-raw-source="[t (Trace)](t--trace-.md)">t (Trace)</a></strong></p></td>
<td align="left"><img src="images/tbinto.png" alt="Screen shot of the Step Into button" /></td>
<td align="left"><p><a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">调试 |单步执行</a></p></td>
<td align="left"><p>F11</p>
<p>F8</p></td>
<td align="left"><p>目标执行一条指令。 如果此指令是函数调用，调试器将跟踪到该调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="ta--trace-to-address-.md" data-raw-source="[ta (Trace to Address)](ta--trace-to-address-.md)">ta （跟踪到地址）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行，直到它达到指定的地址。 显示此函数和调用的函数中的所有步骤。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tb--trace-to-next-branch-.md" data-raw-source="[tb (Trace to Next Branch)](tb--trace-to-next-branch-.md)">tb （跟踪到下一个分支）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>（除内核模式下，仅在基于 x86 的系统上所有模式）目标执行，直到它达到下一步的分支指令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="tc--trace-to-next-call-.md" data-raw-source="[tc (Trace to Next Call)](tc--trace-to-next-call-.md)">tc (到下一步调用 Trace)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>直到出现下一个执行目标<strong>调用</strong>指令。 如果当前指令<strong>调用</strong>指令，该指令跟踪到之前的新<strong>调用</strong>为止。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tct--trace-to-next-call-or-return-.md" data-raw-source="[tct (Trace to Next Call or Return)](tct--trace-to-next-call-or-return-.md)">tct (到下一个调用或返回的 Trace)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行，直到它达到<strong>调用</strong>指令或<strong>返回</strong>指令。 如果当前指令<strong>调用</strong>指令或<strong>返回</strong>指令，该指令跟踪到之前的新<strong>调用</strong>或<strong>返回</strong>为止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="th--trace-to-next-branching-instruction-.md" data-raw-source="[th (Trace to Next Branching Instruction)](th--trace-to-next-branching-instruction-.md)">日 （到下一步的分支指令的跟踪）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行，直到它达到包括条件分支指令的任何类型或无条件分支，调用返回，并且系统调用。 如果当前指令的分支指令，该指令被跟踪到，直到达到新的分支指令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="tt--trace-to-next-return-.md" data-raw-source="[tt (Trace to Next Return)](tt--trace-to-next-return-.md)">tt (到下一步返回的 Trace)</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>目标执行，直到它达到<strong>返回</strong>指令。 如果当前指令<strong>返回</strong>指令，该指令跟踪到之前的新<strong>返回</strong>为止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="wt--trace-and-watch-data-.md" data-raw-source="[wt (Trace and Watch Data)](wt--trace-and-watch-data-.md)">wt （跟踪和查看数据）</a></strong></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>直到整个指定的函数完成执行目标。 然后显示统计信息。</p></td>
</tr>
</tbody>
</table>

 

有关如何重新启动目标计算机的详细信息，请参阅[崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

### <a name="span-idcommandlineoptionsspanspan-idcommandlineoptionsspancommand-line-options"></a><span id="command_line_options"></span><span id="COMMAND_LINE_OPTIONS"></span>命令行选项

如果不希望应用程序停止立即启动或加载时，使用 CDB 或一起使用 WinDbg **-g**命令行选项。 有关这种情况的详细信息，请参阅[初始断点](initial-breakpoint.md)。

此外支持 CDB 和 WinDbg **-G** [命令行选项](command-line-options.md)。 此选项将导致调试会话结束如果应用程序正确完成。

以下命令会尝试从开始到结束，运行该应用程序并仅当发生错误，会显示调试器提示。

```console
cdb -g -G ApplicationName 
```

可以使用 **-pt** [命令行选项](command-line-options.md)设置中断的超时值。没有可以使目标无法与调试器进行通信的某些问题。 如果发出换行命令和调试程序不能中断到目标中，在此时间后，调试器将显示"已被侵入的情形超时"消息。

在此情况下，调试器将停止尝试分解为目标。 相反，调试器将暂停目标，并使您能够检查 （但不是控制） 的目标应用程序。

默认超时为 30 秒。

 

 





