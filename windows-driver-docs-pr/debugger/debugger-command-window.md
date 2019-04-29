---
title: 在 WinDbg 中输入调试器命令
description: 在 WinDbg 中使用调试器命令窗口输入调试器命令
ms.assetid: 4d839170-efaf-43d5-a81c-ac3b9c33586c
keywords: 调试信息 windows 命令窗口中，WinDbg
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: abe50b414433ac31028a55e6ea0ee2c49092c817
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376904"
---
# <a name="entering-debugger-commands-in-windbg"></a>在 WinDbg 中输入调试器命令


## <span id="ddk_debugger_command_window_dbg"></span><span id="DDK_DEBUGGER_COMMAND_WINDOW_DBG"></span>


调试器命令窗口是在 WinDbg 中主要的调试信息窗口。 您可以输入的调试器命令，在此窗口中查看命令输出。

**请注意**  此窗口的标题栏中显示"命令"。 但是，本文档中始终是指"调试器命令窗口"作为此窗口以避免混淆与用于发出 Microsoft MS-DOS 命令的命令提示符窗口。

 

### <a name="span-idopeningthedebuggercommandwindowspanspan-idopeningthedebuggercommandwindowspanopening-the-debugger-command-window"></a><span id="opening_the_debugger_command_window"></span><span id="OPENING_THE_DEBUGGER_COMMAND_WINDOW"></span>打开调试器命令窗口

若要打开调试器命令窗口，请选择**命令**从**视图**菜单。 (还可以按 ALT + 1，或单击**命令**按钮 (![调试器命令窗口按钮的屏幕截图](images/tbcmd.png)) 工具栏上。 ALT + SHIFT + 1 关闭调试器命令窗口。）

下面的屏幕截图显示了调试器的命令窗口的一个示例。

![调试器命令窗口的一个示例的屏幕截图](images/window-command.png)

### <a name="span-idusingthedebuggercommandwindowspanspan-idusingthedebuggercommandwindowspanusing-the-debugger-command-window"></a><span id="using_the_debugger_command_window"></span><span id="USING_THE_DEBUGGER_COMMAND_WINDOW"></span>使用调试器命令窗口

调试器命令窗口拆分为两个窗格。 在窗口底部的小窗格 （命令项窗格） 中键入命令，并在更大窗口的顶部窗格中查看输出。

在命令项窗格中，使用向上键和向下箭头键可以滚动查看命令历史记录。 命令出现时，可以对其进行编辑，或按 enter 键以运行命令。

调试器命令窗口包含带有其他命令的快捷菜单。 若要访问此菜单中，右键单击该窗口的标题栏或单击窗口 （在右上角附近的图标![用于访问调试器命令窗口工具栏快捷方式菜单按钮的屏幕截图 ](images/tbcmd.png))。 以下列表介绍了一些菜单命令：

-   **将添加到命令输出**将注释添加到命令输出中，类似于[编辑 |将添加到命令输出](edit---add-to-command-output.md)命令。

-   **清除命令输出**将删除所有窗口中的文本。

-   **选择文本颜色和克选择...** 打开一个对话框，可用于选择要在其中显示调试器命令窗口中选择的文本的文本颜色。

-   **自动换行**开启和关闭 word 自动换行状态。 此命令会影响整个窗口，不仅使用后选择此状态的命令。 因为许多命令和扩展生成带格式的显示，不建议使用自动换行。

-   **将标记当前位置**在命令窗口中当前游标位置设置一个标记。 该标记的名称是行的右侧光标的内容。

-   **转到将标记**将使窗口滚动，以便包含所选的标记的行是否定位在窗口的顶部。

-   **始终浮点**使窗口保持未停靠，即使拖到停靠位置。

-   **移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。

 

 





