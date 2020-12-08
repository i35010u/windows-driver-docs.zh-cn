---
title: 工具栏按钮
description: 工具栏按钮
keywords:
- 工具栏 (WinDbg) 、按钮说明
- " (WinDbg 工具栏) 的按钮、说明"
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca02c6afd15dd1cb30b2ae02f0c98d0cf6a8da7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811251"
---
# <a name="toolbar-buttons"></a>工具栏按钮


## <span id="ddk_toolbar_buttons_dbg"></span><span id="DDK_TOOLBAR_BUTTONS_DBG"></span>


除了 "断点" 按钮，工具栏上的每个按钮都等效于菜单命令。 有关每个按钮效果的完整说明，请参阅对应菜单命令的页面。

工具栏上的按钮具有以下效果：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Button</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><img src="images/tbopen.png" alt="Screen shot of the Open Source File button" /></td>
<td align="left"><p>将源文件作为只读文件打开。 等效于 <a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">文件 |打开源文件</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcut.png" alt="Screen shot of the Cut button" /></td>
<td align="left"><p>删除活动窗口中的选定文本，并将其放在剪贴板上。 等效于 <a href="edit---cut.md" data-raw-source="[Edit | Cut](edit---cut.md)">编辑 |剪切</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbcopy.png" alt="Screen shot of the Copy button" /></td>
<td align="left"><p>将所选文本从活动窗口复制到剪贴板。 等效于 <a href="edit---copy.md" data-raw-source="[Edit | Copy](edit---copy.md)">编辑 |复制</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbpaste.png" alt="Screen shot of the Paste button" /></td>
<td align="left"><p>将剪贴板上的文本粘贴到光标所在位置。 等效于 <a href="edit---paste.md" data-raw-source="[Edit | Paste](edit---paste.md)">编辑 |粘贴</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbgo.png" alt="Screen shot of the Go button" /></td>
<td align="left"><p>开始或继续执行。 执行将继续，直到到达断点、发生异常或事件、进程结束或调试器进入目标。 等效于 <a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">Debug |继续</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbrestart.png" alt="Screen shot of the Restart button" /></td>
<td align="left"><p>在进程开始时重启执行。 等效于 <a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">Debug |重新启动</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbstop.png" alt="Screen shot of the Stop Debugging button" /></td>
<td align="left"><p>停止执行并永久终止目标进程。 等效于 <a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">Debug |停止调试</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbbreak.png" alt="Screen shot of the Break button" /></td>
<td align="left"><p>在用户模式下，此按钮将停止进程及其线程。 在内核模式下，此按钮会中断目标计算机。 控制返回到调试器。 此按钮还有助于缩短长时间 <a href="the-debugger-command-window.md" data-raw-source="[Debugger Command window](the-debugger-command-window.md)">调试器命令窗口</a> 显示。 等效于 <a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">Debug |中断</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbinto.png" alt="Screen shot of the Step Into button" /></td>
<td align="left"><p>执行一个指令。 如果指令为函数调用，则调试器将逐步进入函数。 等效于 <a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">Debug |单步执行</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbover.png" alt="Screen shot of the Step Over button" /></td>
<td align="left"><p>执行一个指令。 如果指令是函数调用，则调试器将执行整个函数。 等效于 <a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">Debug |逐过程执行</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbout.png" alt="Screen shot of the Step Out button" /></td>
<td align="left"><p>执行当前函数的其余部分，并在函数返回完成后中断。 等效于 <a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">Debug |跳出</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcursor.png" alt="Screen shot of the Run to Cursor button" /></td>
<td align="left"><p>执行从当前指令到 "活动反汇编" 窗口或 "源" 窗口中标记的指令的所有说明。 等效于 <a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">Debug |运行至光标处</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbbp.png" alt="Screen shot of the Breakpoints button" /></td>
<td align="left"><p><strong>如果活动窗口为源窗口或反汇编窗口，则为：</strong> 在当前行中插入一个断点。  (如果在当前行上已设置了一个断点，则此按钮将删除该断点。 ) </p>
<p><strong>否则：</strong> 打开 " <strong>断点</strong> " 对话框，如 " <a href="edit---breakpoints.md" data-raw-source="[Edit | Breakpoints](edit---breakpoints.md)">编辑 |断点</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcmd.png" alt="Screen shot of the Command button" /></td>
<td align="left"><p>打开或激活 <a href="the-debugger-command-window.md" data-raw-source="[Debugger Command](the-debugger-command-window.md)">调试器命令</a> 窗口。 等效于 <a href="view---command.md" data-raw-source="[View | Command](view---command.md)">View |命令</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbwatch.png" alt="Screen shot of the Watch button" /></td>
<td align="left"><p>打开或激活监视窗口。 等效于 <a href="view---watch.md" data-raw-source="[View | Watch](view---watch.md)">View |观看</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tblocal.png" alt="Screen shot of the Locals button" /></td>
<td align="left"><p>打开或激活 "局部变量" 窗口。 等效于 <a href="view---locals.md" data-raw-source="[View | Locals](view---locals.md)">View |局部变量</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbreg.png" alt="Screen shot of the Registers button" /></td>
<td align="left"><p>打开或激活 "寄存器" 窗口。 等效于 <a href="view---registers.md" data-raw-source="[View | Registers](view---registers.md)">View |注册</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbmem.png" alt="Screen shot of the Memory button" /></td>
<td align="left"><p>打开一个新的内存窗口。 等效于 <a href="view---memory.md" data-raw-source="[View | Memory](view---memory.md)">View |内存</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbcall.png" alt="Screen shot of the Call Stack button" /></td>
<td align="left"><p>打开或激活 "调用" 窗口。 等效于 <a href="view---call-stack.md" data-raw-source="[View | Call Stack](view---call-stack.md)">View |调用堆栈</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbdisasm2.png" alt="Screen shot of the Disassembly button" /></td>
<td align="left"><p>打开或激活 "反汇编" 窗口。 等效于 <a href="view---disassembly.md" data-raw-source="[View | Disassembly](view---disassembly.md)">View |反汇编</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbspad.png" alt="Screen shot of the Scratch Pad button" /></td>
<td align="left"><p>打开或激活暂存板。 等效于 <a href="view---scratch-pad.md" data-raw-source="[View | Scratch Pad](view---scratch-pad.md)">View |暂存板</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbsrcasm.png" alt="Screen shot of the Source Mode button" /></td>
<td align="left"><p>在源模式和程序集模式调试之间切换。 等效于选择或清除 " <a href="debug---source-mode.md" data-raw-source="[Debug | Source Mode](debug---source-mode.md)">调试" |源模式</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbfont.png" alt="Screen shot of the Font button" /></td>
<td align="left"><p>使您能够更改在 "调试信息" 窗口中使用的字体。 等效于 <a href="view---font.md" data-raw-source="[View | Font](view---font.md)">View |字体</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbopt.png" alt="Screen shot of the Options button" /></td>
<td align="left"><p>显示 " <strong>选项</strong> " 对话框。 等效于 <a href="view---options.md" data-raw-source="[View | Options](view---options.md)">View |选项</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





