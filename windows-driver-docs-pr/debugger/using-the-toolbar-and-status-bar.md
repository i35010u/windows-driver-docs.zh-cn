---
title: 使用工具栏和状态栏
description: 使用工具栏和状态栏
ms.assetid: 96427166-b6df-4f6b-b550-69d0eb33042d
keywords:
- 工具栏 (WinDbg)
- 工具栏 (WinDbg) 概述
- 按钮 （WinDbg 工具栏）
- 按钮 （WinDbg 工具栏） 概述
- 状态栏
- 状态栏概述
- WinDbg、 工具栏
- WinDbg 状态栏
- WinDbg 中按钮
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54d95640ccb586e68ab50324107fa9ac298aa917
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340513"
---
# <a name="using-the-toolbar-and-status-bar"></a>使用工具栏和状态栏


## <span id="ddk_using_the_toolbar_and_status_bar_dbg"></span><span id="DDK_USING_THE_TOOLBAR_AND_STATUS_BAR_DBG"></span>


*工具栏*附近 WinDbg 窗口的顶部的菜单栏下方会显示。 *状态栏*WinDbg 窗口底部将显示。

### <a name="span-idusingthetoolbarspanspan-idusingthetoolbarspanusing-the-toolbar"></a><span id="using_the_toolbar"></span><span id="USING_THE_TOOLBAR"></span>使用工具栏

下面的屏幕截图显示了 WinDbg 工具栏。

![windbg 工具栏的屏幕截图](images/toolbar4.png)

工具栏按钮具有各种效果。 它们大多数都是等效于菜单命令。 若要执行与工具栏按钮相关联的命令，请单击工具栏按钮。 当您不能使用一个按钮时，它显示为不可用。

有关每个按钮的详细信息，请参阅[工具栏按钮](toolbar-buttons.md)。

### <a name="span-idusingthestatusbarspanspan-idusingthestatusbarspanusing-the-status-bar"></a><span id="using_the_status_bar"></span><span id="USING_THE_STATUS_BAR"></span>使用状态栏

下面的屏幕截图显示了 WinDbg 状态栏。

![windbg 状态栏的屏幕截图](images/statusbar3.png)

下表说明了 WinDbg 状态栏的各个部分。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">部分</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>消息</p></td>
<td align="left"><p>显示在调试器中的消息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Ln，列</p></td>
<td align="left"><p>中处于活动状态的光标所在处显示的行号和列号<a href="source-window.md" data-raw-source="[Source window](source-window.md)">源窗口</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Sys</p></td>
<td align="left"><p>显示正在调试系统的内部十进制数字后接其计算机名称 (或<strong>&lt;本地&gt;</strong>如果它与相同的计算机上运行调试器)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>进程内</p></td>
<td align="left"><p>显示正在调试的进程的内部十进制数字后面是其十六进制进程 id。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Thrd</p></td>
<td align="left"><p>显示正在调试的线程的内部十进制数字后面是其十六进制线程 id。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ASM</p></td>
<td align="left"><p>指示 WinDbg 在程序集模式下。 如果 ASM 不可用，WinDbg 是在源模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OVR</p></td>
<td align="left"><p>指示改写模式处于活动状态。 如果改写不可用，则插入模式处于活动状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CAPS</p></td>
<td align="left"><p>指示已启用了 CAPS LOCK 键。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NUM</p></td>
<td align="left"><p>指示已启用 NUM LOCK。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhidingthetoolbarorstatusbarspanspan-idhidingthetoolbarorstatusbarspanhiding-the-toolbar-or-status-bar"></a><span id="hiding_the_toolbar_or_status_bar"></span><span id="HIDING_THE_TOOLBAR_OR_STATUS_BAR"></span>隐藏工具栏或状态栏

若要显示或隐藏工具栏，请选择或清除[工具栏](view---toolbar.md)上**视图**菜单。 若要显示或隐藏状态栏，请选择或清除[状态栏](view---status-bar.md)上**视图**菜单。

如果隐藏工具栏或状态栏，则可以调试 windows 在 WinDbg 中的显示区域的信息的更多空间。

### <a name="span-idsettingthewindowtitlespanspan-idsettingthewindowtitlespansetting-the-window-title"></a><span id="setting_the_window_title"></span><span id="SETTING_THE_WINDOW_TITLE"></span>设置窗口标题

可以使用更改 WinDbg 窗口的标题[ **.wtitle （设置窗口标题）** ](-wtitle--set-window-title-.md)命令。

 

 





