---
title: 键盘快捷键
description: 键盘快捷键
keywords:
- 控制键，WinDbg 快捷键
- WinDbg，快捷键
- 快捷键
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49aaf9684e768bcbd0c84a7fb3bca7c0efff70af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806549"
---
# <a name="keyboard-shortcuts"></a>键盘快捷键


## <span id="ddk_shortcut_keys_dbg"></span><span id="DDK_SHORTCUT_KEYS_DBG"></span>


您可以使用以下键盘快捷方式在窗口之间进行切换。 有关如何在窗口之间移动的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">键</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Ctrl+Tab</p></td>
<td align="left"><p>在调试信息窗口之间切换。 通过重复使用此密钥，您可以扫描所有窗口，而不管它们是浮动、停靠还是固定窗口的一部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt+Tab</p></td>
<td align="left"><p>在当前桌面上的窗口之间进行切换。 你还可以使用此键盘快捷方式在 WinDbg 帧和你已创建的任何其他停靠之间切换。</p></td>
</tr>
</tbody>
</table>

 

您可以使用以下键盘快捷方式，而不是使用鼠标来选择菜单命令。 有关每个命令的详细信息，请参阅各个命令主题。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">键</th>
<th align="left">菜单等效项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>F1</p></td>
<td align="left"><p><a href="help---contents.md" data-raw-source="[Help | Contents](help---contents.md)">帮助 | 内容</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F3</p></td>
<td align="left"><p><a href="edit---find-next.md" data-raw-source="[Edit | Find Next](edit---find-next.md)">编辑 | 查找下一个</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHIFT+F3</p></td>
<td align="left"><p>与 " <a href="edit---find-next.md" data-raw-source="[Edit | Find Next](edit---find-next.md)">编辑" 相同 |查找下一个</a>，除非按相反的方向执行搜索。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt + F4</p></td>
<td align="left"><p><a href="file---exit.md" data-raw-source="[File | Exit](file---exit.md)">文件 | 退出</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+F4</p></td>
<td align="left"><p><a href="file---close-current-window.md" data-raw-source="[File | Close Current Window](file---close-current-window.md)">文件 | 关闭当前窗口</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F5</p></td>
<td align="left"><p><a href="debug---go.md" data-raw-source="[Debug | Go](debug---go.md)">调试 | 转到</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Shift+F5</p></td>
<td align="left"><p><a href="debug---stop-debugging.md" data-raw-source="[Debug | Stop Debugging](debug---stop-debugging.md)">调试 | 停止调试</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+Shift+F5</p></td>
<td align="left"><p><a href="debug---restart.md" data-raw-source="[Debug | Restart](debug---restart.md)">调试 | 重启</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>F6</p></td>
<td align="left"><p><a href="file---attach-to-a-process.md" data-raw-source="[File | Attach to a Process](file---attach-to-a-process.md)">文件 | 附加到进程</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F7</p></td>
<td align="left"><p><a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">调试 | 运行到光标处</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>F8</p></td>
<td align="left"><p><a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">调试 | 跳入</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F9</p></td>
<td align="left"><p>如果活动窗口为源窗口或反汇编窗口，则：在当前行插入一个断点。  (如果在当前行上已设置了一个断点，则此按钮将删除该断点。 ) </p>
<p>否则：打开 " <strong>断点</strong> " 对话框，如 " <a href="edit---breakpoints.md" data-raw-source="[Edit | Breakpoints](edit---breakpoints.md)">编辑 |断点</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Alt+F9</p></td>
<td align="left"><p><a href="edit---breakpoints.md" data-raw-source="[Edit | Breakpoints](edit---breakpoints.md)">编辑 | 断点</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F10</p></td>
<td align="left"><p><a href="debug---step-over.md" data-raw-source="[Debug | Step Over](debug---step-over.md)">调试 | 逐步运行</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+F10</p></td>
<td align="left"><p><a href="debug---run-to-cursor.md" data-raw-source="[Debug | Run to Cursor](debug---run-to-cursor.md)">调试 | 运行到光标处</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>F11</p></td>
<td align="left"><p><a href="debug---step-into.md" data-raw-source="[Debug | Step Into](debug---step-into.md)">调试 | 跳入</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHIFT+F11</p></td>
<td align="left"><p><a href="debug---step-out.md" data-raw-source="[Debug | Step Out](debug---step-out.md)">调试 | 跳出</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt+1</p></td>
<td align="left"><p>打开 <a href="debugger-command-window.md" data-raw-source="[Debugger Command window](debugger-command-window.md)">调试器命令窗口</a> 与 View (相同 <a href="view---command.md" data-raw-source="[View | Command](view---command.md)">|命令</a>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 1</p></td>
<td align="left"><p>关闭命令窗口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt+2</p></td>
<td align="left"><p>打开与视图相同的监视窗口 (<a href="view---watch.md" data-raw-source="[View | Watch](view---watch.md)">|观看</a>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 2</p></td>
<td align="left"><p>关闭监视窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt+3</p></td>
<td align="left"><p>打开 " <a href="locals-window.md" data-raw-source="[Locals window](locals-window.md)">局部变量" 窗口</a> (与 "视图" 相同 <a href="view---locals.md" data-raw-source="[View | Locals](view---locals.md)">|局部变量</a>) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 3</p></td>
<td align="left"><p>关闭 "局部变量" 窗口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt+4</p></td>
<td align="left"><p>打开 " <a href="registers-window.md" data-raw-source="[Registers window](registers-window.md)">寄存器" 窗口</a> (与 "视图" 相同 <a href="view---registers.md" data-raw-source="[View | Registers](view---registers.md)">|注册</a>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 4</p></td>
<td align="left"><p>关闭 "寄存器" 窗口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 5</p></td>
<td align="left"><p>打开新的 " <a href="memory-window.md" data-raw-source="[Memory window](memory-window.md)">内存" 窗口</a> (与 "视图" 相同 <a href="view---memory.md" data-raw-source="[View | Memory](view---memory.md)">|内存</a>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 5</p></td>
<td align="left"><p>关闭 "内存" 窗口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt+6</p></td>
<td align="left"><p>打开与视图 (相同的 " <a href="calls-window.md" data-raw-source="[Calls window](calls-window.md)">调用" 窗口</a> <a href="view---call-stack.md" data-raw-source="[View | Call Stack](view---call-stack.md)">|调用堆栈</a>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 6</p></td>
<td align="left"><p>关闭调用窗口</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt+7</p></td>
<td align="left"><p>打开 " <a href="disassembly-window.md" data-raw-source="[Disassembly window](disassembly-window.md)">反汇编" 窗口</a> (与 "视图" 相同 <a href="view---disassembly.md" data-raw-source="[View | Disassembly](view---disassembly.md)">|反汇编</a>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 7</p></td>
<td align="left"><p>关闭 "反汇编" 窗口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Alt+8</p></td>
<td align="left"><p> (相同的视图打开暂存板 <a href="view---scratch-pad.md" data-raw-source="[View | Scratch Pad](view---scratch-pad.md)">|) 的暂存板</a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 8</p></td>
<td align="left"><p>关闭暂存板。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + 9</p></td>
<td align="left"><p>打开 " <a href="processes-and-threads-window.md" data-raw-source="[Processes and Threads window](processes-and-threads-window.md)">进程和线程" 窗口</a> (与 "视图" 相同 <a href="view---processes-and-threads.md" data-raw-source="[View | Processes and Threads](view---processes-and-threads.md)">|) 的进程和线程</a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ALT + SHIFT + 9</p></td>
<td align="left"><p>关闭 "进程和线程" 窗口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+A</p></td>
<td align="left"><p><a href="edit---select-all.md" data-raw-source="[Edit | Select All](edit---select-all.md)">编辑 | 全选</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+C</p></td>
<td align="left"><p><a href="edit---copy.md" data-raw-source="[Edit | Copy](edit---copy.md)">编辑 | 复制</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+D</p></td>
<td align="left"><p><a href="file---open-crash-dump.md" data-raw-source="[File | Open Crash Dump](file---open-crash-dump.md)">文件 | 打开故障转储</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+E</p></td>
<td align="left"><p><a href="file---open-executable.md" data-raw-source="[File | Open Executable](file---open-executable.md)">文件 | 打开可执行文件</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+F</p></td>
<td align="left"><p><a href="edit---find.md" data-raw-source="[Edit | Find](edit---find.md)">编辑 | 查找</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+G</p></td>
<td align="left"><p><a href="edit---go-to-address.md" data-raw-source="[Edit | Go to Address](edit---go-to-address.md)">编辑 | 转到地址</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL+I</p></td>
<td align="left"><p><a href="file---image-file-path.md" data-raw-source="[File | Image File Path](file---image-file-path.md)">文件 | 映像文件路径</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+Shift+I</p></td>
<td align="left"><p><a href="edit---set-current-instruction.md" data-raw-source="[Edit | Set Current Instruction](edit---set-current-instruction.md)">编辑 | 设置当前指令</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+K</p></td>
<td align="left"><p><a href="file---kernel-debug.md" data-raw-source="[File | Kernel Debug](file---kernel-debug.md)">文件 | 内核调试</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+L</p></td>
<td align="left"><p><a href="edit---go-to-line.md" data-raw-source="[Edit | Go to Line](edit---go-to-line.md)">编辑 | 转到行</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+O</p></td>
<td align="left"><p><a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">文件 | 打开源文件</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+P</p></td>
<td align="left"><p><a href="file---source-file-path.md" data-raw-source="[File | Source File Path](file---source-file-path.md)">文件 | 源文件路径</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+R</p></td>
<td align="left"><p><a href="file---connect-to-remote-session.md" data-raw-source="[File | Connect to Remote Session](file---connect-to-remote-session.md)">文件 | 连接到远程会话</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+S</p></td>
<td align="left"><p><a href="file---symbol-file-path.md" data-raw-source="[File | Symbol File Path](file---symbol-file-path.md)">文件 | 符号文件路径</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+V</p></td>
<td align="left"><p><a href="edit---paste.md" data-raw-source="[Edit | Paste](edit---paste.md)">编辑 | 粘贴</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+Shift+V</p></td>
<td align="left"><p><a href="edit---evaluate-selection.md" data-raw-source="[Edit | Evaluate Selection](edit---evaluate-selection.md)">编辑 | 评估所选内容</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+W</p></td>
<td align="left"><p><a href="file---open-workspace.md" data-raw-source="[File | Open Workspace](file---open-workspace.md)">文件 | 打开工作区</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+X</p></td>
<td align="left"><p><a href="edit---cut.md" data-raw-source="[Edit | Cut](edit---cut.md)">编辑 | 剪切</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + SHIFT + Y</p></td>
<td align="left"><p><a href="edit---display-selected-type.md" data-raw-source="[Edit | Display Selected Type](edit---display-selected-type.md)">编辑 | 显示所选类型</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
ALT + <strong>*</strong> (数字键盘) </td>
<td align="left"><p><a href="edit---go-to-current-instruction.md" data-raw-source="[Edit | Go to Current Instruction](edit---go-to-current-instruction.md)">编辑 | 转到当前指令</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Shift+Delete</p></td>
<td align="left"><p><a href="edit---cut.md" data-raw-source="[Edit | Cut](edit---cut.md)">编辑 | 剪切</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Shift+Insert</p></td>
<td align="left"><p><a href="edit---paste.md" data-raw-source="[Edit | Paste](edit---paste.md)">编辑 | 粘贴</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+Insert</p></td>
<td align="left"><p><a href="edit---copy.md" data-raw-source="[Edit | Copy](edit---copy.md)">编辑 | 复制</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+Break</p></td>
<td align="left"><p><a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">调试 | 中断</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ALT + DEL</p></td>
<td align="left"><p><a href="debug---break.md" data-raw-source="[Debug | Break](debug---break.md)">调试 | 中断</a></p></td>
</tr>
</tbody>
</table>

 

以下快捷键等效于 KD/CDB 控件键。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">键</th>
<th align="left">菜单等效项</th>
<th align="left">KD/CDB 控制键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Ctrl+Alt+A</p></td>
<td align="left"><p><a href="debug---kernel-connection---cycle-baud-rate.md" data-raw-source="[Debug | Kernel Connection | Cycle Baud Rate](debug---kernel-connection---cycle-baud-rate.md)">调试 | 内核连接 | 循环波特率</a></p></td>
<td align="left"><p>Ctrl+A</p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL+ALT+D</p></td>
<td align="left"></td>
<td align="left"><p><strong><a href="ctrl-d--toggle-debug-info-.md" data-raw-source="[CTRL+D (Toggle Debug Info)](ctrl-d--toggle-debug-info-.md)">CTRL+D（切换调试信息）</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ctrl+Alt+K</p></td>
<td align="left"><p><a href="debug---kernel-connection---cycle-initial-break.md" data-raw-source="[Debug | Kernel Connection | Cycle Initial Break](debug---kernel-connection---cycle-initial-break.md)">调试 | 内核连接 | 循环初始中断</a></p></td>
<td align="left"><p>Ctrl+K</p></td>
</tr>
<tr class="even">
<td align="left"><p>Ctrl+Alt+R</p></td>
<td align="left"><p><a href="debug---kernel-connection---resynchronize.md" data-raw-source="[Debug | Kernel Connection | Resynchronize](debug---kernel-connection---resynchronize.md)">调试 | 内核连接 | 重新同步</a></p></td>
<td align="left"><p>Ctrl+R</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTRL + ALT + V</p></td>
<td align="left"><p><a href="view---verbose-output.md" data-raw-source="[View | Verbose Output](view---verbose-output.md)">视图 | 详细输出</a></p></td>
<td align="left"><p>Ctrl+V</p></td>
</tr>
<tr class="even">
<td align="left"><p>CTRL + ALT + W</p></td>
<td align="left"><p><a href="view---show-version.md" data-raw-source="[View | Show Version](view---show-version.md)">视图 | 显示版本</a></p></td>
<td align="left"><p>Ctrl+W</p></td>
</tr>
</tbody>
</table>

 

你可以使用以下键盘快捷方式在大多数调试信息窗口中移动 ^)  (^。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">插入符号移动</th>
<th align="left">键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>向左一个字符</p></td>
<td align="left"><p>LEFT</p></td>
</tr>
<tr class="even">
<td align="left"><p>向右一个字符</p></td>
<td align="left"><p>RIGHT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>左移单词</p></td>
<td align="left"><p>CTRL + 向左键</p></td>
</tr>
<tr class="even">
<td align="left"><p>右移单词</p></td>
<td align="left"><p>CTRL + 向右键</p></td>
</tr>
<tr class="odd">
<td align="left"><p>向上移动一行</p></td>
<td align="left"><p>UP</p></td>
</tr>
<tr class="even">
<td align="left"><p>向下移动一行</p></td>
<td align="left"><p>DOWN</p></td>
</tr>
<tr class="odd">
<td align="left"><p>向上翻页</p></td>
<td align="left"><p>Page Up</p></td>
</tr>
<tr class="even">
<td align="left"><p>向下翻页</p></td>
<td align="left"><p>Page Down</p></td>
</tr>
<tr class="odd">
<td align="left"><p>当前行的开头</p></td>
<td align="left"><p>Home</p></td>
</tr>
<tr class="even">
<td align="left"><p>行尾</p></td>
<td align="left"><p>End</p></td>
</tr>
<tr class="odd">
<td align="left"><p>文件开头</p></td>
<td align="left"><p>Ctrl+Home</p></td>
</tr>
<tr class="even">
<td align="left"><p>文件结尾</p></td>
<td align="left"><p>Ctrl+End</p></td>
</tr>
</tbody>
</table>

 

**注意**   在 [调试器命令窗口](debugger-command-window.md)中，按向上键和向下键可浏览命令历史记录。 可以使用 INSERT 键打开和关闭插入模式。

 

使用以下键盘快捷方式选择文本。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Select</th>
<th align="left">键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>左移字符</p></td>
<td align="left"><p>SHIFT + 向左键</p></td>
</tr>
<tr class="even">
<td align="left"><p>右移字符</p></td>
<td align="left"><p>SHIFT + 向右键</p></td>
</tr>
<tr class="odd">
<td align="left"><p>左移单词</p></td>
<td align="left"><p>SHIFT + CTRL + 向左键</p></td>
</tr>
<tr class="even">
<td align="left"><p>右移单词</p></td>
<td align="left"><p>SHIFT + CTRL + 向右键</p></td>
</tr>
<tr class="odd">
<td align="left"><p>当前行</p></td>
<td align="left"><p>如果在第1列中插入符号，则按 SHIFT + 向下键</p></td>
</tr>
<tr class="even">
<td align="left"><p>上方线条</p></td>
<td align="left"><p>如果在第1列中插入符号，则按 SHIFT + 向上键</p></td>
</tr>
<tr class="odd">
<td align="left"><p>到行尾</p></td>
<td align="left"><p>Shift+End</p></td>
</tr>
<tr class="even">
<td align="left"><p>到行的开头</p></td>
<td align="left"><p>Shift+Home</p></td>
</tr>
<tr class="odd">
<td align="left"><p>屏幕向上</p></td>
<td align="left"><p>SHIFT + PAGE UP</p></td>
</tr>
<tr class="even">
<td align="left"><p>屏幕向下</p></td>
<td align="left"><p>SHIFT + Page Down</p></td>
</tr>
<tr class="odd">
<td align="left"><p>到文件开头</p></td>
<td align="left"><p>SHIFT + CTRL + HOME</p></td>
</tr>
<tr class="even">
<td align="left"><p>结束文件</p></td>
<td align="left"><p>SHIFT + CTRL + END</p></td>
</tr>
</tbody>
</table>

 

使用以下键盘快捷方式删除文本。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">删除</th>
<th align="left">键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>插入符号右边的字符</p></td>
<td align="left"><p>DELETE</p></td>
</tr>
<tr class="even">
<td align="left"><p>插入符号左侧的字符</p></td>
<td align="left"><p>Backspace</p></td>
</tr>
<tr class="odd">
<td align="left"><p>选定的文本</p></td>
<td align="left"><p>DELETE</p></td>
</tr>
</tbody>
</table>

 

 

 





