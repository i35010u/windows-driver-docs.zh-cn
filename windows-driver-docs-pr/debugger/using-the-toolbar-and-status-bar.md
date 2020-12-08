---
title: 使用工具栏和状态栏
description: 使用工具栏和状态栏
keywords:
- " (WinDbg) 工具栏"
- 工具栏 (WinDbg) ，概述
- '按钮 (WinDbg 工具栏) '
- 按钮 (WinDbg 工具栏) ，概述
- 状态栏
- 状态栏，概述
- WinDbg，工具栏
- WinDbg，状态栏
- WinDbg、按钮
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba2306d8bf775c2cb36354e50961927b5bf52829
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803017"
---
# <a name="using-the-toolbar-and-status-bar"></a>使用工具栏和状态栏


## <span id="ddk_using_the_toolbar_and_status_bar_dbg"></span><span id="DDK_USING_THE_TOOLBAR_AND_STATUS_BAR_DBG"></span>


*工具栏* 将显示在菜单栏的下方，位于 WinDbg 窗口的顶部附近。 *状态栏* 显示在 "WinDbg" 窗口的底部。

### <a name="span-idusing_the_toolbarspanspan-idusing_the_toolbarspanusing-the-toolbar"></a><span id="using_the_toolbar"></span><span id="USING_THE_TOOLBAR"></span>使用工具栏

以下屏幕截图显示了 WinDbg 工具栏。

![windbg 工具栏的屏幕截图](images/toolbar4.png)

工具栏按钮具有各种效果。 其中大多数等效于菜单命令。 若要执行与工具栏按钮相关联的命令，请单击工具栏按钮。 不能使用按钮时，它将不可用。

有关每个按钮的详细信息，请参阅 [工具栏按钮](toolbar-buttons.md)。

### <a name="span-idusing_the_status_barspanspan-idusing_the_status_barspanusing-the-status-bar"></a><span id="using_the_status_bar"></span><span id="USING_THE_STATUS_BAR"></span>使用状态栏

下面的屏幕截图显示了 WinDbg 状态栏。

![windbg 状态栏的屏幕截图](images/statusbar3.png)

下表介绍了 WinDbg 状态栏的各个部分。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">部分</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>消息</p></td>
<td align="left"><p>显示来自调试器的消息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Ln、Col</p></td>
<td align="left"><p>显示光标在活动 <a href="source-window.md" data-raw-source="[Source window](source-window.md)">源窗口</a>中的行号和列号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Sys</p></td>
<td align="left"><p>显示正在调试的系统的内部十进制数，后跟计算机名称 (或<strong> &lt; 本地 &gt; </strong> （如果它与调试器在) 上运行时的计算机名称相同）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Proc</p></td>
<td align="left"><p>显示要调试的进程的内部十进制数，后跟其十六进制进程 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Thrd</p></td>
<td align="left"><p>显示正在调试的线程的内部十进制数，后跟其十六进制线程 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ASM</p></td>
<td align="left"><p>指示 WinDbg 处于组件模式。 如果 ASM 不可用，则 WinDbg 处于源模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OVR</p></td>
<td align="left"><p>指示改写模式处于活动状态。 如果 OVR 不可用，则插入模式处于活动状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>帽</p></td>
<td align="left"><p>指示 Caps Lock 为 on。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>编号</p></td>
<td align="left"><p>指示 NUM LOCK 处于开启。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhiding_the_toolbar_or_status_barspanspan-idhiding_the_toolbar_or_status_barspanhiding-the-toolbar-or-status-bar"></a><span id="hiding_the_toolbar_or_status_bar"></span><span id="HIDING_THE_TOOLBAR_OR_STATUS_BAR"></span>隐藏工具栏或状态栏

若要显示或隐藏工具栏，请在 "**视图**" 菜单上选择或清除 "[工具栏](view---toolbar.md)"。 若要显示或隐藏状态栏，请在 "**视图**" 菜单上选择或清除 "[状态栏](view---status-bar.md)"。

如果隐藏工具栏或状态栏，则在 WinDbg 显示区域中有更多空间用于调试信息窗口。

### <a name="span-idsetting_the_window_titlespanspan-idsetting_the_window_titlespansetting-the-window-title"></a><span id="setting_the_window_title"></span><span id="SETTING_THE_WINDOW_TITLE"></span>设置窗口标题

您可以使用 [**. wtitle (设置窗口标题)**](-wtitle--set-window-title-.md) 命令更改 WinDbg 窗口的标题。

 

 





