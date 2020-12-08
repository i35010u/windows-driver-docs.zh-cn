---
title: 打开窗口
description: 打开窗口
keywords:
- 调试信息窗口，打开
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e65d5c0f5c75a38bcea385553b15f084802a85e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798393"
---
# <a name="opening-a-window"></a>打开窗口


## <span id="ddk_opening_a_window_dbg"></span><span id="DDK_OPENING_A_WINDOW_DBG"></span>


当 WinDbg 开始调试会话时， [调试器命令窗口](debugger-command-window.md) 会自动打开。 "[反汇编" 窗口](disassembly-window.md)还会自动打开，除非取消选择 "**窗口**" 菜单上的 "[自动打开反汇编](window---automatically-open-disassembly.md)"。

当 WinDbg 发现与当前程序计数器对应的源文件时，WinDbg 将打开该文件的 [源窗口](source-window.md) 。 有关打开源窗口的其他方式，请参阅 [源路径](source-path.md)。

您可以使用以下菜单命令、工具栏按钮和快捷键切换到这些窗口。 也就是说，如果窗口未打开，则打开它。 如果某个窗口处于打开状态但处于非活动状态，则它将变为活动状态。 如果停靠窗口并且它前面有一个浮动窗口，则停靠窗口将变为活动状态，但浮动窗口将停留在停靠窗口之前。

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
<th align="left">快捷键</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="debugger-command-window.md" data-raw-source="[Debugger Command window](debugger-command-window.md)">调试器命令窗口</a></p></td>
<td align="left"><p><strong>视图 | 命令</strong></p></td>
<td align="left"><img src="images/tbcmd.png" alt="Screen shot of the Debugger Command window button" /></td>
<td align="left"><p>Alt+1</p></td>
</tr>
<tr class="even">
<td align="left"><p>监视窗口</p></td>
<td align="left"><p><strong>视图 | 监视</strong></p></td>
<td align="left"><img src="images/tbwatch.png" alt="Screen shot of the Watch button" /></td>
<td align="left"><p>Alt+2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="locals-window.md" data-raw-source="[Locals window](locals-window.md)">局部变量窗口</a></p></td>
<td align="left"><p><strong>视图 | 局部变量</strong></p></td>
<td align="left"><img src="images/tblocal.png" alt="Screen shot of the Locals button" /></td>
<td align="left"><p>Alt+3</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="registers-window.md" data-raw-source="[Registers window](registers-window.md)">注册窗口</a></p></td>
<td align="left"><p><strong>视图 | 寄存器</strong></p></td>
<td align="left"><img src="images/tbreg.png" alt="Screen shot of the Registers button" /></td>
<td align="left"><p>Alt+4</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="memory-window.md" data-raw-source="[Memory window](memory-window.md)">“内存”窗口</a></p></td>
<td align="left"><p><strong>视图 | 内存</strong></p></td>
<td align="left"><img src="images/tbmem.png" alt="Screen shot of the Memory button" /></td>
<td align="left"><p>ALT + 5</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="calls-window.md" data-raw-source="[Calls window](calls-window.md)">调用窗口</a></p></td>
<td align="left"><p><strong>视图 | 调用堆栈</strong></p></td>
<td align="left"><img src="images/tbcall.png" alt="Screen shot of the Call Stack button" /></td>
<td align="left"><p>Alt+6</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="disassembly-window.md" data-raw-source="[Disassembly window](disassembly-window.md)">“反汇编”窗口</a></p></td>
<td align="left"><p><strong>视图 | 反汇编</strong></p></td>
<td align="left"><img src="images/tbdisasm2.png" alt="Screen shot of the Disassembly button" /></td>
<td align="left"><p>Alt+7</p></td>
</tr>
<tr class="even">
<td align="left"><p>"暂存板" 窗口</p></td>
<td align="left"><p><strong>视图 | 暂存器</strong></p></td>
<td align="left"><img src="images/tbspad.png" alt="Screen shot of the Scratch Pad button" /></td>
<td align="left"><p>Alt+8</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="processes-and-threads-window.md" data-raw-source="[Processes and Threads window](processes-and-threads-window.md)">"进程和线程" 窗口</a></p></td>
<td align="left"><p><strong>视图 | 进程和线程</strong></p></td>
<td align="left"><img src="images/window-processes-threads.png" alt="Screen shot of the Processes and Threads button" /></td>
<td align="left"><p>ALT + 9</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="source-window.md" data-raw-source="[Source window](source-window.md)">源窗口</a></p></td>
<td align="left"><p>单击 " <a href="file---open-source-file.md" data-raw-source="[File | Open Source File](file---open-source-file.md)">文件" |打开源文件</a> ，然后选择一个源文件。</p></td>
<td align="left"><img src="images/tbopen.png" alt="Screen shot of the Open Source File button" /></td>
<td align="left"><p>Ctrl+O</p></td>
</tr>
</tbody>
</table>

 

你还可以通过从 "**窗口**" 菜单底部的 "打开窗口"[列表](list-of-open-windows.md)中选择窗口来激活窗口。

 

 





