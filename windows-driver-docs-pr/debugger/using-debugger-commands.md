---
title: 使用调试器命令
description: 本部分介绍如何使用调试器命令。 输入命令提示符窗口的底部。
ms.assetid: 64dcc364-53b5-41d3-9266-abcfe4b328f4
keywords: 命令、 调试器命令和元命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77bf91529add011f250f17e483bc37311015597b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527169"
---
# <a name="using-debugger-commands"></a>使用调试器命令


## <span id="ddk_using_debugger_commands_dbg"></span><span id="DDK_USING_DEBUGGER_COMMANDS_DBG"></span>


对于 KD 或 CDB，"调试器命令窗口"是指整个窗口。 输入命令提示符窗口的底部。 如果命令有任何输出，窗口将显示输出，然后再次显示提示符。

有关 Visual Studio 中，"调试器命令窗口"是指一个窗口，其中在标题栏中标记为"调试器即时窗口"。 此窗口具有两个窗格：

-   在小型的底部窗格中，输入命令。

-   在大型、 上部窗格中，您可以查看命令输出。

有关的 WinDbg 中，"调试器命令窗口"是指将在标题栏中标记为"命令"窗口。 此窗口包含两个窗格：

-   在小型的底部窗格中，输入命令。

-   在大型、 上部窗格中，您可以查看命令输出。

调试会话开始时已始终打开此窗口。 您可以重新打开或切换到此窗口，通过单击**命令**上**视图**菜单中，按 ALT + 1，或单击**命令 (Alt + 1)** 按钮 (![屏幕截图调试器命令窗口按钮的](images/tbcmd.png)) 工具栏上。

可以使用向上键和向下箭头键可以滚动查看命令历史记录。 前一命令出现时，可以对其进行编辑，然后按 ENTER 以执行前一命令 （或上一命令的已编辑的版本）。 游标没有要在此过程才能正常工作行的末尾。

### <a name="span-iddebuggercommandwindowpromptspanspan-iddebuggercommandwindowpromptspandebugger-command-window-prompt"></a><span id="debugger_command_window_prompt"></span><span id="DEBUGGER_COMMAND_WINDOW_PROMPT"></span>调试器命令窗口提示符

当执行用户模式下时调试在调试器命令提示符窗口类似于下面的示例。

`2:005>`

在前面的示例中，2 是当前的进程数，和 005 是当前的线程数。

如果将调试器附加到多台计算机，进程和线程数，如以下示例所示之前包括系统编号。

`3:2:005>`

在此示例中，3 是当前的系统编号，2 是当前进程号，005 是当前的线程数。

时要执行内核模式调试的目标计算机只有一个处理器上，提示符类似于下面的示例。

`kd>`

但是，如果目标计算机具有多个处理器，出现提示时，如以下示例所示之前就会显示当前的处理器数。

`0: kd> `

如果调试器正忙于处理以前颁发的命令，新的命令将暂时不会处理，尽管可以将它们添加到命令缓冲区。 此外，仍可以使用[控制密钥](control-keys.md)在 KD 和 CDB，和你仍然可以使用菜单命令和[键盘快捷方式](keyboard-shortcuts.md)在 WinDbg 中。 当 KD 或 CDB 处于此忙碌状态时，不显示任何提示。 此忙碌状态 WinDbg 时，将取代在提示符下显示以下指标：

`*BUSY* `

可以使用[ **.pcmd （设置在命令提示符）** ](-pcmd--set-prompt-command-.md)命令将文本添加到此提示。

### <a name="span-idkindsofcommandsspanspan-idkindsofcommandsspankinds-of-commands"></a><span id="kinds_of_commands"></span><span id="KINDS_OF_COMMANDS"></span>类型的命令

WinDbg 和 KD、 CDB 支持不同的命令。 调试器之间共享的一些命令，而有些则仅在一个或两个调试器上可用。

仅在实时调试中，有一些命令和其他命令仅在调试转储文件后才可用。

仅在用户模式下调试过程提供了一些命令，并仅在内核模式调试过程提供了其他命令。

只有当目标特定的处理器上运行时提供了一些命令。 有关的所有命令和它们的限制的详细信息，请参阅[调试器命令](debugger-commands.md)。

### <a name="span-ideditingrepeatingandcancelingcommandsspanspan-ideditingrepeatingandcancelingcommandsspanediting-repeating-and-canceling-commands"></a><span id="editing__repeating__and_canceling_commands"></span><span id="EDITING__REPEATING__AND_CANCELING_COMMANDS"></span>编辑、 重复和取消命令

当你输入命令时，可以使用标准的编辑键：

-   使用向上键和向下箭头键来查找前面的命令。

-   使用退格符、 DELETE、 INSERT 和向左键和向右箭头键编辑当前命令。

-   按 ESC 键以清除当前行。

可以按 TAB 键自动完成文本输入。 在任何调试程序中，输入至少一个字符来自动完成命令后按 TAB 键。 按 TAB 键重复以循环文本完成选项，并按住 SHIFT 键并按 tab 键向后循环。 此外可以在文本中使用通配符，并按 TAB 展开为完整的文本完成选项集。 例如，如果键入**fo\*！ ba** ，然后按 TAB 键，调试器将扩展到开头"ba"模块名称以"fo"开头的所有模块中的所有符号的集。 作为另一个示例中，你可以完成通过键入中都有"prcb"的所有扩展命令 **！\*prcb** ，然后按 TAB。

当使用 TAB 键来执行文本完成功能，如果文本片段以句点 （.） 开头时，会将文本与点命令进行匹配。 如果文本片段以带感叹号 （！），则会将文本与扩展命令进行匹配。 否则，与符号匹配文本。 当您使用 TAB 键输入符号，按 TAB 键完成代码和类型符号和模块名称。 如果没有模块名称是很明显，完成本地符号和模块名称。 如果未指定模块或模块模式，符号完成完成中的所有匹配项的代码和类型符号。

您可以右键单击来自动粘贴剪贴板的内容到正在键入的命令在调试器命令窗口中。

最大命令长度为 4096 个字符。 但是，如果要[控制用户模式下的调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)，最大行长度为 512 个字符。

在 CDB 和 KD，本身重复前一命令中按 ENTER 键。 在 WinDbg 中，可以启用或禁用此行为。 有关此行为的详细信息，请参阅[ **ENTER （重复执行最后一个命令）**](enter--repeat-last-command-.md)。

如果您发出的最后一个命令显示长，并且你想要关闭使用剪切[ **CTRL + C** ](ctrl-c--break-.md) CDB 或 KD 中的键。 在 WinDbg 中，使用[调试 |中断](debug---break.md)或按 CTRL + BREAK。

在内核模式调试中，可以从目标计算机的键盘命令取消通过按[ **CTRL + C**](ctrl-c--break-.md)。

可以使用[ **.cls （清除屏幕）** ](-cls--clear-screen-.md)命令，以清除所有从文本[调试器命令窗口](debugger-command-window.md)。 此命令将清除整个命令历史记录。 在 WinDbg 中，可以通过使用清除命令历史记录[编辑 |清除命令输出](edit---clear-command-output.md)命令，或通过单击**清除命令输出**调试器命令窗口的快捷菜单上。

### <a name="span-idexpressionsyntaxspanspan-idexpressionsyntaxspanexpression-syntax"></a><span id="expression_syntax"></span><span id="EXPRESSION_SYNTAX"></span>表达式语法

许多命令和扩展命令接受*表达式*作为其参数。 调试器执行命令前将计算这些表达式。 有关表达式的详细信息，请参阅[评估表达式](evaluating-expressions.md)。

### <a name="span-idaliasesspanspan-idaliasesspanaliases"></a><span id="aliases"></span><span id="ALIASES"></span>别名

*别名*是可用于避免无需重新键入复杂的短语的文本宏。 有两种类型的别名。 有关别名的详细信息，请参阅[Using 别名](using-aliases.md)。

### <a name="span-idselfrepeatingcommandsspanspan-idselfrepeatingcommandsspanself-repeating-commands"></a><span id="self_repeating_commands"></span><span id="SELF_REPEATING_COMMANDS"></span>自重复命令

可以使用以下命令以重复执行操作或有条件地执行其他命令：

-   [ **J (执行 If-else)** ](j--execute-if---else-.md)条件命令

-   [ **Z （执行时）** ](z--execute-while-.md)条件命令

-   [ **~ E （特定于线程的命令）** ](-e--thread-specific-command-.md)命令限定符

-   [ **！ 列表**](-list.md)扩展命令

有关每个命令的详细信息，请参阅单个命令主题。

### <a name="span-idcontrollingscrollingspanspan-idcontrollingscrollingspancontrolling-scrolling"></a><span id="controlling_scrolling"></span><span id="CONTROLLING_SCROLLING"></span>控制滚动

可以使用滚动条来查看上一命令和相应的输出。

当使用 CDB 或 KD 时，自动使调试器命令窗口返回到底部的向下滚动任何键盘输入。

在 WinDbg 中，显示，自动滚动到底部的命令生成的输出或按 ENTER 键时。 如果你想要禁用此自动滚动，单击[选项](view---options.md)上**视图**菜单，然后清除**自动滚动**复选框。

### <a name="span-idwindbgtextfeaturesspanspan-idwindbgtextfeaturesspanwindbg-text-features"></a><span id="windbg_text_features"></span><span id="WINDBG_TEXT_FEATURES"></span>WinDbg 文本功能

在 WinDbg 中，可以使用其他几项功能，若要更改文本中的显示方式[调试器命令窗口](debugger-command-window.md)。 可以访问一些 WinDbg 窗口中的这些功能，一些在调试器命令窗口中，在快捷菜单和一些通过单击相应的菜单图标。

-   **自动换行**命令的快捷菜单上，开启和关闭 word 自动换行状态。 此命令会影响整个窗口，不仅能使用此状态更改后的命令。 由于许多命令和扩展生成带格式的显示，我们通常不建议自动换行。

-   [编辑 |将添加到命令输出](edit---add-to-command-output.md)菜单命令在调试器命令窗口中添加注释。 **将添加到命令输出**快捷菜单上的命令具有相同的效果。

-   可以自定义用于文本和调试器命令窗口的背景的颜色。 可以指定不同的颜色不同类型的文本。 例如，可以在另一种颜色，显示的一种颜色中的自动注册输出、 错误消息和**DbgPrint**中的消息的第三个颜色。 有关此自定义的详细信息，请参阅[视图 |选项](view---options.md)。

-   您可以使用的所有常见功能到 WinDbg 的调试信息窗口，如自定义字体和使用特殊的编辑命令。 有关这些功能的详细信息，请参阅[使用调试信息 Windows](using-debugging-information-windows.md)。

### <a name="span-idremotedebuggingspanspan-idremotedebuggingspanremote-debugging"></a><span id="remote_debugging"></span><span id="REMOTE_DEBUGGING"></span>远程调试

当您在执行远程调试通过调试器时，调试客户端可以访问有限的数量的命令。 若要更改的客户端可以访问的命令数，请使用 **-clines** [命令行选项](command-line-options.md)或\_NT\_调试\_历史记录\_大小[环境变量](environment-variables.md)。

 

 





