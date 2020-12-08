---
title: 视图选项
description: 视图选项
keywords:
- 视图选项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9ae4c9c202c94794ffc5f7c10c56e16773961dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833157"
---
# <a name="view--options"></a>视图 | 选项


## <span id="ddk_view_options_dbg"></span><span id="DDK_VIEW_OPTIONS_DBG"></span>


单击 "**查看**" 菜单上的 "**选项**" 以打开 "**选项**" 对话框。 此命令等效于在工具栏上单击 " ![ 选项" 按钮)  (屏幕截图的按钮 ](images/tbopt.png) 。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

在 " **选项** " 对话框中，可以选择或取消选择以下选项：

<span id="Tab_width"></span><span id="tab_width"></span><span id="TAB_WIDTH"></span>**选项卡宽度**  
" **选项卡宽度** " 框控制选项卡字符在任何源窗口中的显示方式。 在 " **选项卡宽度** " 框中，输入要在每个选项卡设置之间设置的空格数。  (默认设置为8。 有关文本属性的详细信息，请参阅 [更改文本属性](changing-text-properties.md)。 ) 

<span id="Reuse_after_opening_this_many"></span><span id="reuse_after_opening_this_many"></span><span id="REUSE_AFTER_OPENING_THIS_MANY"></span>**打开此多个**  
**打开此多个框后的重复使用** 控制可同时打开的文档或源窗口的数量。 如果已达到指定的源窗口数，打开新窗口将导致现有窗口关闭。 标记为选项卡停靠目标的窗口不会关闭。 最近使用的窗口是最近使用过的窗口。

<span id="Parse_source_languages"></span><span id="parse_source_languages"></span><span id="PARSE_SOURCE_LANGUAGES"></span>**分析源语言**  
如果选择了 " **分析源语言** " 复选框，则所有源窗口中的源代码文本都将根据源语法的简单分析来着色。 若要更改颜色，请在对话框的 " **颜色** " 区域中，选择一个语法元素，然后单击 " **更改**"。  (在单个源窗口中关闭语法颜色，请打开该窗口的快捷菜单，单击 "**选择源语言**"，然后单击 " **&lt; 无 &gt;**"。 ) 

<span id="Evaluate_on_hover"></span><span id="evaluate_on_hover"></span><span id="EVALUATE_ON_HOVER"></span>**悬停时计算**  
如果选中了 " **在悬停时计算** " 复选框 (并且) 选中了 " **分析源语言** " 复选框，则在您选择该窗口并使用鼠标将鼠标悬停在某个符号上时，将计算源窗口中的符号。 此计算与 [**dt (显示类型)**](dt--display-type-.md) 命令生成的值相同。

<span id="Enter_repeats_last_command"></span><span id="enter_repeats_last_command"></span><span id="ENTER_REPEATS_LAST_COMMAND"></span>**输入重复的最后一个命令**  
如果选中了 " **输入重复的最后一个命令** " 复选框，则可以在调试器中的空提示符下按 enter 键 [命令窗口](debugger-command-window.md) 以重复上一个命令。 如果清除此复选框，则 ENTER 键会生成新的提示。

<span id="Automatically_scroll"></span><span id="automatically_scroll"></span><span id="AUTOMATICALLY_SCROLL"></span>**自动滚动**  
" **自动滚动** " 复选框控制在将新文本发送到调试器命令窗口时所发生的自动滚动。 如果要关闭此功能，请清除 " **自动滚动** " 复选框。 有关此滚动的详细信息，请参阅 [使用调试器命令](using-debugger-commands.md)。

<span id="Workspace_Prompts"></span><span id="workspace_prompts"></span><span id="WORKSPACE_PROMPTS"></span>**工作区提示**  
在 " **工作区提示** " 区域中，可以单击三个选项之一，以确定在 WinDbg 中保存工作区的时间和频率。

-   如果单击 " **始终询问**"，当工作区发生更改时 (例如) 调试会话结束时，调试器将显示 " **工作区保存** " 对话框，你可以在其中保存工作区。

    在 " **工作区保存** " 对话框中，如果单击 " **不再询问**"，WinDbg 会将 " **工作区提示** " 选项重置为 " **永不保存** " 或 " **始终保存**"。

-   如果单击 " **始终保存**"，则会在工作区发生更改时自动将其保存。

-   如果单击 " **永不保存**"，则工作区将不会在更改时保存，并且不会提示您保存它。

<span id="QuickEdit_Mode"></span><span id="quickedit_mode"></span><span id="QUICKEDIT_MODE"></span>**快速编辑模式**  
如果选择了 " **编辑模式** " 复选框，则可以右键单击要复制或粘贴的项，具体取决于窗口选择状态。 如果清除此复选标记，则会禁用 "快速编辑"，您可以右键单击某个项目以打开该窗口的快捷菜单。 不能为各个 windows 单独设置。"快速编辑" 设置适用于所有窗口。 默认情况下，此框处于选中状态。 "快速编辑" 设置将保存在当前工作区中。

<span id="Colors"></span><span id="colors"></span><span id="COLORS"></span>**颜色**  
若要更改显示的源文本的颜色，请在 " **颜色** " 区域中选择一个项，然后单击 " **更改**"。 选择一种颜色，或选择一种自定义颜色，然后单击 **"确定"**。

在 " **颜色** " 菜单中，可以更改以下各项的颜色：

-   前十个项表示 "反汇编" [窗口](disassembly-window.md) 和 " [源" 窗口](source-window.md)中的文本。

-   已 **更改的数据文本** 项表示已更改的数据条目 (例如，在 " [寄存器" 窗口](registers-window.md) 中) 。

-   十个 **源** *Xxx* 项控制用于源窗口中的语法元素的颜色。

-   其余项引用调试器中的不同类型的文本命令窗口。

单击 **"确定"** 后，这些颜色更改将生效。 若要放弃这些更改，请单击 " **取消**"。

 

 





