---
title: 工具栏按钮
description: 工具栏按钮
ms.assetid: a32702fe-28c5-4b41-b4da-9a750946e5dd
keywords:
- 工具栏 (WinDbg) 按钮说明
- 按钮 （WinDbg 工具栏） 说明
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dedb2317b96cce548b21a95744cf50fed1f5dbc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556086"
---
# <a name="toolbar-buttons"></a>工具栏按钮


## <span id="ddk_toolbar_buttons_dbg"></span><span id="DDK_TOOLBAR_BUTTONS_DBG"></span>


除了断点按钮在工具栏上的每个按钮相当于菜单命令。 每个按钮的效果的完整说明，请参阅相应的菜单命令的页。

在工具栏上的按钮具有以下效果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">按钮</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><img src="images/tbopen.png" alt="Screen shot of the Open Source File button" /></td>
<td align="left"><p>打开源文件为只读的文件。 等效于<a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">文件 |打开源文件</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcut.png" alt="Screen shot of the Cut button" /></td>
<td align="left"><p>从活动窗口中删除所选的文本并将其放到剪贴板上。 等效于<a href="edit---cut.md" data-raw-source="[Edit | Cut](edit---cut.md)">编辑 |剪切</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbcopy.png" alt="Screen shot of the Copy button" /></td>
<td align="left"><p>将所选的文本从活动窗口复制到剪贴板。 等效于<a href="edit---copy.md" data-raw-source="[Edit | Copy](edit---copy.md)">编辑 |复制</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbpaste.png" alt="Screen shot of the Paste button" /></td>
<td align="left"><p>将文本粘贴到光标所在的位置在剪贴板上。 等效于<a href="edit---paste.md" data-raw-source="[Edit | Paste](edit---paste.md)">编辑 |粘贴</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbgo.png" alt="Screen shot of the Go button" /></td>
<td align="left"><p>启动或恢复执行。 执行将继续到达到断点、 异常或事件发生时，该过程结束或调试器将中断目标。 等效于<a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">调试 |转</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbrestart.png" alt="Screen shot of the Restart button" /></td>
<td align="left"><p>重新启动进程的开始处的执行。 等效于<a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">调试 |重新启动</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbstop.png" alt="Screen shot of the Stop Debugging button" /></td>
<td align="left"><p>停止执行并永久终止目标进程。 等效于<a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">调试 |停止调试</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbbreak.png" alt="Screen shot of the Break button" /></td>
<td align="left"><p>在用户模式下，此按钮停止进程和线程。 在内核模式下，此按钮将分成在目标计算机。 控制权返回给调试器。 此按钮也是用于长时间切断<a href="the-debugger-command-window.md" data-raw-source="[Debugger Command window](the-debugger-command-window.md)">调试器命令窗口</a>显示。 等效于<a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">调试 |中断</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbinto.png" alt="Screen shot of the Step Into button" /></td>
<td align="left"><p>执行一条指令。 如果指令为函数调用，调试器将单步执行函数。 等效于<a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">调试 |单步执行</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbover.png" alt="Screen shot of the Step Over button" /></td>
<td align="left"><p>执行一条指令。 如果指令是函数调用，调试器将在一个步骤中执行整个函数。 等效于<a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">调试 |逐过程执行</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbout.png" alt="Screen shot of the Step Out button" /></td>
<td align="left"><p>执行当前函数的其余部分，并完成函数返回时中断。 等效于<a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">调试 |跳出</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcursor.png" alt="Screen shot of the Run to Cursor button" /></td>
<td align="left"><p>从当前到标记为活动反汇编窗口或源窗口中的指令指令执行的所有说明。 等效于<a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">调试 |运行到光标处</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbbp.png" alt="Screen shot of the Breakpoints button" /></td>
<td align="left"><p><strong>如果活动窗口的源或反汇编窗口：</strong>在当前行中插入断点。 （如果已没有当前行上设置断点，此按钮将移除该断点。）</p>
<p><strong>否则为：</strong>此时将打开<strong>断点</strong>像那样的对话框<a href="edit---breakpoints.md" data-raw-source="[Edit | Breakpoints](edit---breakpoints.md)">编辑 |断点</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbcmd.png" alt="Screen shot of the Command button" /></td>
<td align="left"><p>打开或激活<a href="the-debugger-command-window.md" data-raw-source="[Debugger Command](the-debugger-command-window.md)">调试器命令</a>窗口。 等效于<a href="view---command.md" data-raw-source="[View | Command](view---command.md)">视图 |命令</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbwatch.png" alt="Screen shot of the Watch button" /></td>
<td align="left"><p>打开或激活监视窗口。 等效于<a href="view---watch.md" data-raw-source="[View | Watch](view---watch.md)">视图 |观看</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tblocal.png" alt="Screen shot of the Locals button" /></td>
<td align="left"><p>打开或激活局部变量窗口。 等效于<a href="view---locals.md" data-raw-source="[View | Locals](view---locals.md)">视图 |局部变量</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbreg.png" alt="Screen shot of the Registers button" /></td>
<td align="left"><p>打开或激活寄存器窗口。 等效于<a href="view---registers.md" data-raw-source="[View | Registers](view---registers.md)">视图 |注册</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbmem.png" alt="Screen shot of the Memory button" /></td>
<td align="left"><p>打开一个新的内存窗口。 等效于<a href="view---memory.md" data-raw-source="[View | Memory](view---memory.md)">视图 |内存</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbcall.png" alt="Screen shot of the Call Stack button" /></td>
<td align="left"><p>打开或激活调用窗口。 等效于<a href="view---call-stack.md" data-raw-source="[View | Call Stack](view---call-stack.md)">视图 |调用堆栈</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbdisasm2.png" alt="Screen shot of the Disassembly button" /></td>
<td align="left"><p>打开或激活反汇编窗口。 等效于<a href="view---disassembly.md" data-raw-source="[View | Disassembly](view---disassembly.md)">视图 |反汇编</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbspad.png" alt="Screen shot of the Scratch Pad button" /></td>
<td align="left"><p>打开或激活暂存器。 等效于<a href="view---scratch-pad.md" data-raw-source="[View | Scratch Pad](view---scratch-pad.md)">视图 |草稿板</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbsrcasm.png" alt="Screen shot of the Source Mode button" /></td>
<td align="left"><p>源模式和调试程序集模式之间切换。 等效于选中或清除<a href="debug---source-mode.md" data-raw-source="[Debug | Source Mode](debug---source-mode.md)">调试 |源模式</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><img src="images/tbfont.png" alt="Screen shot of the Font button" /></td>
<td align="left"><p>可以更改在调试的信息窗口中使用的字体。 等效于<a href="view---font.md" data-raw-source="[View | Font](view---font.md)">视图 |字体</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><img src="images/tbopt.png" alt="Screen shot of the Options button" /></td>
<td align="left"><p>显示<strong>选项</strong>对话框。 等效于<a href="view---options.md" data-raw-source="[View | Options](view---options.md)">视图 |选项</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





