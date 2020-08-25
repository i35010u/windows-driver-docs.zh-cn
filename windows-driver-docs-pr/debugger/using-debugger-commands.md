---
title: 使用调试器命令
description: 本部分介绍如何使用调试器命令。 在窗口底部的提示符下输入命令。
ms.assetid: 64dcc364-53b5-41d3-9266-abcfe4b328f4
keywords: 命令，调试器命令，元命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eda0b83310158a373655ec71425b87e20e72c683
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802499"
---
# <a name="using-debugger-commands"></a>使用调试器命令


## <span id="ddk_using_debugger_commands_dbg"></span><span id="DDK_USING_DEBUGGER_COMMANDS_DBG"></span>


对于 KD 或 CDB，"调试器命令窗口" 指的是整个窗口。 在窗口底部的提示符下输入命令。 如果命令有任何输出，则该窗口将显示输出，并再次显示该提示。

对于 Visual Studio，"调试器命令窗口" 是指标题栏中标记为 "调试器即时窗口" 的窗口。 此窗口有两个窗格：

-   在小的底部窗格中，输入命令。

-   在大、上部窗格中，你可以查看命令输出。

对于 WinDbg，"调试器命令窗口" 是指标题栏中标记为 "Command" 的窗口。 此窗口包含两个窗格：

-   在小的底部窗格中，输入命令。

-   在大、上部窗格中，你可以查看命令输出。

此窗口始终在调试会话开始时打开。 通过选择 "**视图**" 菜单上的 "**命令**"，按 ALT + 1，或在工具栏上的 "调试器命令窗口" 按钮)  (屏幕截图** (alt + 1) ** "按钮，可以重新打开或切换到此窗口 ![ ](images/tbcmd.png) 。

您可以使用向上键和向下键在命令历史记录中滚动。 出现上一个命令后，可以编辑它，然后按 ENTER 执行上一个命令 (或) 的上一个命令的编辑版本。 光标不一定要位于行的末尾，此过程才能正常工作。

### <a name="span-iddebugger_command_window_promptspanspan-iddebugger_command_window_promptspandebugger-command-window-prompt"></a><span id="debugger_command_window_prompt"></span><span id="DEBUGGER_COMMAND_WINDOW_PROMPT"></span>调试器命令窗口提示

执行用户模式调试时，调试器中的提示符命令窗口如下面的示例所示。

`2:005>`

在前面的示例中，2是当前进程编号，而005是当前线程号。

如果将调试器附加到多台计算机，则系统号将包含在进程和线程号之前，如以下示例中所示。

`3:2:005>`

在此示例中，3是当前系统号，2是当前进程编号，005是当前线程号。

当你在只有一个处理器的目标计算机上执行内核模式调试时，提示符将如以下示例中所示。

`kd>`

但是，如果目标计算机有多个处理器，则当前处理器的数目将显示在提示符之前，如下面的示例中所示。

`0: kd> `

如果调试器忙于处理以前发出的命令，则不会处理新命令，但可以将其添加到命令缓冲区中。 此外，还可以在 KD 和 CDB 中使用 [控制键](control-keys.md) ，并且仍可以在 WinDbg 中使用菜单命令和 [快捷键](keyboard-shortcuts.md) 。 当 KD 或 CDB 处于此繁忙状态时，不会显示提示。 当 WinDbg 处于此繁忙状态时，将显示以下指示器来代替提示符：

`*BUSY* `

你可以使用 [**. pcmd (Set Prompt 命令) **](-pcmd--set-prompt-command-.md) 命令向此提示符中添加文本。

### <a name="span-idkinds_of_commandsspanspan-idkinds_of_commandsspankinds-of-commands"></a><span id="kinds_of_commands"></span><span id="KINDS_OF_COMMANDS"></span>命令种类

WinDbg、KD 和 CDB 支持多种命令。 某些命令在调试器之间共享，某些命令仅在一个或两个调试器上可用。

某些命令仅可用于实时调试，而其他命令仅在调试转储文件时可用。

某些命令仅在用户模式调试期间可用，而其他命令仅在内核模式调试过程中可用。

某些命令仅在目标在特定处理器上运行时才可用。 有关所有命令及其限制的详细信息，请参阅 [调试器命令](debugger-commands.md)。

### <a name="span-idediting__repeating__and_canceling_commandsspanspan-idediting__repeating__and_canceling_commandsspanediting-repeating-and-canceling-commands"></a><span id="editing__repeating__and_canceling_commands"></span><span id="EDITING__REPEATING__AND_CANCELING_COMMANDS"></span>编辑、重复和取消命令

输入命令时，可以使用标准编辑键：

-   使用向上键和向下键可查找上一个命令。

-   用 BACKSPACE、DELETE、INSERT、左箭头和右箭头键编辑当前命令。

-   按 ESC 键以清除当前行。

可以按 TAB 键自动完成文本输入。 在任意调试中，在输入至少一个字符后按 TAB 键自动完成命令。 重复按 TAB 键以循环浏览文本完成选项，按住 SHIFT 键，并按 TAB 键向后循环。 你还可以在文本中使用通配符，并按 TAB 键以展开到完整的文本完成选项集。 例如，如果键入 **fo \* ！ ba** ，然后按 tab，则调试器会将以 "ba" 开头的所有符号的集合扩展为以 "fo" 开头的模块名称的所有模块。 作为另一个示例，你可以通过键入 **！ \* 来完成所有扩展名为 "prcb" 的命令：prcb** ，然后按 tab。

使用 TAB 键执行文本完成时，如果文本片段以句点开头 ( ) ，则将文本与点命令匹配。 如果文本片段以感叹号开头 (！ ) ，则文本与扩展命令匹配。 否则，文本将与符号匹配。 当 usee TAB 键输入符号时，按 TAB 键完成代码，然后键入符号和模块名称。 如果没有明显的模块名称，则会完成本地符号和模块名称。 如果给定了模块或模块模式，则符号完成完成代码并键入所有匹配项的符号。

您可以选择并按住 (或右键单击调试器命令窗口) ，以自动将剪贴板的内容粘贴到您正在键入的命令中。

最大命令长度为4096个字符。 但是，如果要 [从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)，则最大行长度为512个字符。

在 CDB 和 KD 中，按 ENTER 键以重复上一个命令。 在 WinDbg 中，可以启用或禁用此行为。 有关此行为的详细信息，请参阅 [**ENTER (重复最后一个命令) **](enter--repeat-last-command-.md)。

如果你发出的最后一个命令显示长时间，并且你想要将其剪切掉，请在 CDB 或 KD 中使用 [**CTRL + C**](ctrl-c--break-.md) 键。 在 WinDbg 中，使用 " [调试" |中断](debug---break.md) 或按 CTRL + break。

在内核模式调试中，可以通过按 [**CTRL + C**](ctrl-c--break-.md)从目标计算机的键盘取消命令。

您可以使用 [**. cls (Clear Screen) **](-cls--clear-screen-.md) 命令从 [调试器命令窗口](debugger-command-window.md)中清除所有文本。 此命令清除整个命令历史记录。 在 WinDbg 中，可以通过使用 " [编辑" |清除 "命令输出](edit---clear-command-output.md) " 命令，或选择调试器的快捷菜单上的 " **清除命令输出** " 命令窗口。

### <a name="span-idexpression_syntaxspanspan-idexpression_syntaxspanexpression-syntax"></a><span id="expression_syntax"></span><span id="EXPRESSION_SYNTAX"></span>表达式语法

许多命令和扩展命令接受 *表达式* 作为其参数。 调试器将在执行命令之前计算这些表达式。 有关表达式的详细信息，请参阅 [计算表达式](evaluating-expressions.md)。

### <a name="span-idaliasesspanspan-idaliasesspanaliases"></a><span id="aliases"></span><span id="ALIASES"></span>别名

*别名* 是文本宏，可用于避免重新键入复杂短语。 有两种类型的别名。 有关别名的详细信息，请参阅 [使用别名](using-aliases.md)。

### <a name="span-idself_repeating_commandsspanspan-idself_repeating_commandsspanself-repeating-commands"></a><span id="self_repeating_commands"></span><span id="SELF_REPEATING_COMMANDS"></span>自重复命令

可以使用以下命令重复操作或有条件地执行其他命令：

-   [**如果-Else) 条件命令，j (执行**](j--execute-if---else-.md)

-   [**当) 条件命令时，z (执行**](z--execute-while-.md)

-   [**~ E (线程特定的命令) **](-e--thread-specific-command-.md)命令限定符

-   [**！ List**](-list.md) extension 命令

有关每个命令的详细信息，请参阅各个命令主题。

### <a name="span-idcontrolling_scrollingspanspan-idcontrolling_scrollingspancontrolling-scrolling"></a><span id="controlling_scrolling"></span><span id="CONTROLLING_SCROLLING"></span>控制滚动

您可以使用滚动条查看以前的命令及其输出。

使用 CDB 或 KD 时，任何键盘输入都将自动向下滚动调试器命令窗口向下滚动。

在 WinDbg 中，每当命令生成输出或按下 ENTER 键时，显示都会自动向下滚动到底部。 如果要禁用此自动滚动，请在 "**视图**" 菜单上选择[选项](view---options.md)，然后清除 "**自动滚动**" 复选框。

### <a name="span-idwindbg_text_featuresspanspan-idwindbg_text_featuresspanwindbg-text-features"></a><span id="windbg_text_features"></span><span id="WINDBG_TEXT_FEATURES"></span>WinDbg 文本功能

在 WinDbg 中，您可以使用几个附加功能来更改文本在调试器中的显示方式 [命令窗口](debugger-command-window.md)。 您可以在 WinDbg 窗口中访问其中的某些功能，在调试器的快捷菜单中命令窗口一些功能，还可以通过选择相应的菜单图标来访问某些功能。

-   快捷菜单上的 " **自动换行** " 命令会打开和关闭 "自动换行" 状态。 此命令会影响整个窗口，而不仅是在此状态更改后使用的命令。 由于许多命令和扩展都生成格式的显示，因此，我们通常不推荐自动换行。

-   [编辑 |"添加到命令输出](edit---add-to-command-output.md)" 菜单命令在调试器命令窗口中添加注释。 快捷菜单上的 " **添加到命令输出** " 命令具有相同的效果。

-   您可以自定义用于文本的颜色和调试器命令窗口的背景。 您可以为不同类型的文本指定不同的颜色。 例如，您可以用一种颜色显示自动注册输出，以另一种颜色显示错误消息，并以第三种颜色 **DbgPrint** 消息。 有关此自定义的详细信息，请参阅 [View |选项](view---options.md)。

-   您可以使用 WinDbg 的调试信息窗口通用的所有功能，例如自定义字体和使用特殊的编辑命令。 有关这些功能的详细信息，请参阅 [使用调试信息窗口](using-debugging-information-windows.md)。

### <a name="span-idremote_debuggingspanspan-idremote_debuggingspanremote-debugging"></a><span id="remote_debugging"></span><span id="REMOTE_DEBUGGING"></span>远程调试

通过调试器执行远程调试时，调试客户端可以访问有限数量的命令。 若要更改客户端可以访问的命令数，请使用 **-clines** [命令行选项](command-line-options.md) 或 " \_ NT \_ 调试 \_ 历史记录 \_ 大小" [环境变量](environment-variables.md)。

 

 





