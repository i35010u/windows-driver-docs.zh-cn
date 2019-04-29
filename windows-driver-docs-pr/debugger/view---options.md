---
title: 视图选项
description: 视图选项
ms.assetid: 2579c586-f1f3-4b03-a47f-22be98fe6c51
keywords:
- 视图选项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86859d492f81fa532a600f5835b7623f586230fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371673"
---
# <a name="view--options"></a>视图 | 选项


## <span id="ddk_view_options_dbg"></span><span id="DDK_VIEW_OPTIONS_DBG"></span>


单击**选项**上**视图**菜单打开**选项**对话框。 此命令等效于单击的按钮 (![选项按钮的屏幕截图](images/tbopt.png)) 工具栏上。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

在中**选项**对话框中，可以选择或取消选择以下选项：

<span id="Tab_width"></span><span id="tab_width"></span><span id="TAB_WIDTH"></span>**选项卡宽度**  
**选项卡宽度**框控制的制表符字符数在任何源窗口中的显示方式。 在中**选项卡宽度**框中，输入你想要具有每个选项卡设置之间的空格数。 （默认设置为 8。 文本属性的详细信息，请参阅[更改文本属性](changing-text-properties.md)。)

<span id="Reuse_after_opening_this_many"></span><span id="reuse_after_opening_this_many"></span><span id="REUSE_AFTER_OPENING_THIS_MANY"></span>**打开此多后重复使用**  
**打开此多后的重用**框控制的文档或源，可以同时打开的窗口数。 如果已达到指定的数目的源窗口，打开一个新的窗口会导致现有窗口关闭。 标记为选项卡形式停靠目标，请不要关闭 Windows。 若要关闭的最后一个 windows 是最近使用的。

<span id="Parse_source_languages"></span><span id="parse_source_languages"></span><span id="PARSE_SOURCE_LANGUAGES"></span>**分析源代码语言**  
如果**分析源语言**复选框处于选中状态，根据 simple 分析的源语法进行着色的所有源窗口中的源代码文本。 若要更改颜色，在**颜色**区域中的对话框中，选择一个语法元素，然后单击**更改**。 (若要在单个源窗口关闭语法颜色，请打开该窗口的快捷菜单，单击**选择源语言**，然后单击 **&lt;None&gt;**。)

<span id="Evaluate_on_hover"></span><span id="evaluate_on_hover"></span><span id="EVALUATE_ON_HOVER"></span>**悬停时的评估**  
如果**悬停时的 Evaluate**复选框处于选中状态 (和**分析源代码语言**同时选中复选框)，将计算源窗口中的符号，当您选择该窗口，然后将鼠标悬停使用鼠标的符号。 计算的是与生成的相同[ **dt （显示类型）** ](dt--display-type-.md)命令。

<span id="Enter_repeats_last_command"></span><span id="enter_repeats_last_command"></span><span id="ENTER_REPEATS_LAST_COMMAND"></span>**输入重复最后一个命令**  
如果**Enter 重复最后一个命令**复选框处于选中状态，可以按 ENTER 键在空中提示[调试器命令窗口](debugger-command-window.md)重复前一命令。 如果清除此复选框，ENTER 键，会生成新提示。

<span id="Automatically_scroll"></span><span id="automatically_scroll"></span><span id="AUTOMATICALLY_SCROLL"></span>**自动滚动**  
**自动滚动**复选框控制自动滚动的新文本发送到调试器命令窗口时发生。 如果你想要关闭此功能，请清除**自动滚动**复选框。 有关此滚动的详细信息，请参阅[使用调试器命令](using-debugger-commands.md)。

<span id="Workspace_Prompts"></span><span id="workspace_prompts"></span><span id="WORKSPACE_PROMPTS"></span>**工作区的提示**  
在中**工作区会提示**区域中，您可以单击三个选项之一来确定时间和频率在 WinDbg 中保存工作区。

-   如果单击**总是询问**，当工作区更改 （例如当调试会话结束时），调试器将显示**工作区保存**对话框中，您可以在其中保存工作区。

    在**工作区保存**对话框中，如果单击**不要再询问**，WinDbg 将重置**工作区会提示**选项设置为**永远不会保存**或**始终保存**。

-   如果单击**始终保存**，发生更改时自动保存在工作区。

-   如果单击**永远不会保存**，工作区时不会保存更改，并不提示将其保存。

<span id="QuickEdit_Mode"></span><span id="quickedit_mode"></span><span id="QUICKEDIT_MODE"></span>**快速编辑模式**  
如果**QuickEdit 模式**复选框处于选中状态，可以右键单击要复制或粘贴到，具体取决于窗口中选择状态的项。 当清除此项检查时，快速编辑已禁用，可以右键单击要打开窗口的快捷菜单的项。 不能为单个窗口提供不同的设置;快速编辑设置全局适用于所有窗口。 默认情况下，选中此框。 快速编辑设置保存在当前工作区中。

<span id="Colors"></span><span id="colors"></span><span id="COLORS"></span>**颜色**  
若要更改显示的源文本的颜色，请选择一项**颜色**然后单击**更改**。 选择一种颜色，或选择自定义颜色，然后单击**确定**。

在中**颜色**菜单中，您可以更改以下各项的颜色：

-   前 10 个项表示中的文本[反汇编窗口](disassembly-window.md)并[源窗口](source-window.md)。

-   **更改数据文本**项表示已更改的数据条目 (例如，在[寄存器窗口](registers-window.md))。

-   前十位**源** *Xxx*项控制用于在源窗口中的语法元素的颜色。

-   剩余的项目引用不同类型的调试器命令窗口中的文本。

这些颜色更改为才会生效，当您单击时**确定**。 若要放弃这些更改，请单击**取消**。

 

 





