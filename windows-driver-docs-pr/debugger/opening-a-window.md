---
title: 打开窗口
description: 打开窗口
ms.assetid: e056a556-8201-47e5-9a21-dbd5277c15c2
keywords:
- 调试信息窗口中打开
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea21ae1b5260054952c351bdb7bfbe60fce2ecfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331037"
---
# <a name="opening-a-window"></a>打开窗口


## <span id="ddk_opening_a_window_dbg"></span><span id="DDK_OPENING_A_WINDOW_DBG"></span>


WinDbg 开始调试会话时[调试器命令窗口](debugger-command-window.md)会自动打开。 [反汇编窗口](disassembly-window.md)还会自动打开，除非取消选择[自动打开反汇编](window---automatically-open-disassembly.md)上**窗口**菜单。

每当 WinDbg 发现对应于当前的程序计数器的源文件，将打开 WinDbg[源窗口](source-window.md)该文件。 有关其他方法可以打开源窗口，请参阅[源路径](source-path.md)。

可以使用以下命令、 工具栏按钮和键盘快捷方式可用于切换到这些窗口。 也就是说，如果窗口未打开，它会打开。 如果一个窗口处于打开但处于非活动状态，它将变为活动状态。 如果没有它的前面的浮动窗口停靠窗口，停靠的窗口将变为活动状态但浮动窗口将保持停靠窗口的前面。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">窗口</th>
<th align="left">菜单命令</th>
<th align="left">Button</th>
<th align="left">键盘快捷方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="debugger-command-window.md" data-raw-source="[Debugger Command window](debugger-command-window.md)">调试器命令窗口</a></p></td>
<td align="left"><p><strong>视图 |命令</strong></p></td>
<td align="left"><img src="images/tbcmd.png" alt="Screen shot of the Debugger Command window button" /></td>
<td align="left"><p>ALT+1</p></td>
</tr>
<tr class="even">
<td align="left"><p>观察时段</p></td>
<td align="left"><p><strong>视图 |监视</strong></p></td>
<td align="left"><img src="images/tbwatch.png" alt="Screen shot of the Watch button" /></td>
<td align="left"><p>ALT+2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="locals-window.md" data-raw-source="[Locals window](locals-window.md)">局部变量窗口</a></p></td>
<td align="left"><p><strong>视图 |局部变量</strong></p></td>
<td align="left"><img src="images/tblocal.png" alt="Screen shot of the Locals button" /></td>
<td align="left"><p>ALT+3</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="registers-window.md" data-raw-source="[Registers window](registers-window.md)">寄存器窗口</a></p></td>
<td align="left"><p><strong>视图 |注册</strong></p></td>
<td align="left"><img src="images/tbreg.png" alt="Screen shot of the Registers button" /></td>
<td align="left"><p>ALT+4</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="memory-window.md" data-raw-source="[Memory window](memory-window.md)">内存窗口</a></p></td>
<td align="left"><p><strong>视图 |内存</strong></p></td>
<td align="left"><img src="images/tbmem.png" alt="Screen shot of the Memory button" /></td>
<td align="left"><p>ALT+5</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="calls-window.md" data-raw-source="[Calls window](calls-window.md)">调用窗口</a></p></td>
<td align="left"><p><strong>视图 |调用堆栈</strong></p></td>
<td align="left"><img src="images/tbcall.png" alt="Screen shot of the Call Stack button" /></td>
<td align="left"><p>ALT+6</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="disassembly-window.md" data-raw-source="[Disassembly window](disassembly-window.md)">反汇编窗口</a></p></td>
<td align="left"><p><strong>视图 |反汇编</strong></p></td>
<td align="left"><img src="images/tbdisasm2.png" alt="Screen shot of the Disassembly button" /></td>
<td align="left"><p>ALT+7</p></td>
</tr>
<tr class="even">
<td align="left"><p>草稿板窗口</p></td>
<td align="left"><p><strong>视图 |草稿板</strong></p></td>
<td align="left"><img src="images/tbspad.png" alt="Screen shot of the Scratch Pad button" /></td>
<td align="left"><p>ALT+8</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="processes-and-threads-window.md" data-raw-source="[Processes and Threads window](processes-and-threads-window.md)">进程和线程窗口</a></p></td>
<td align="left"><p><strong>视图 |进程和线程</strong></p></td>
<td align="left"><img src="images/window-processes-threads.png" alt="Screen shot of the Processes and Threads button" /></td>
<td align="left"><p>ALT+9</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="source-window.md" data-raw-source="[Source window](source-window.md)">源窗口</a></p></td>
<td align="left"><p>单击<a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">文件 |打开源文件</a>，然后选择源文件。</p></td>
<td align="left"><img src="images/tbopen.png" alt="Screen shot of the Open Source File button" /></td>
<td align="left"><p>Ctrl+O</p></td>
</tr>
</tbody>
</table>

 

您还可以通过选择它从激活窗口[打开的窗口的列表](list-of-open-windows.md)底部**窗口**菜单。

 

 





