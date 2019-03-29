---
title: 在 WinDbg 中进行源代码调试
description: 在 WinDbg 中进行源代码调试
ms.assetid: 0f939d29-0d90-442e-96d7-fe756b92a7da
keywords:
- 调试信息窗口中，源窗口
- 源窗口
- 调试时，源窗口的源
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75289348fa8a46cde10ba8faf67d8ee0d962f8df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564695"
---
# <a name="source-code-debugging-in-windbg"></a>在 WinDbg 中进行源代码调试


## <a name="span-idddksourcepathdbgspanspan-idddksourcepathdbgspansource-path"></a><span id="ddk_source_path_dbg"></span><span id="DDK_SOURCE_PATH_DBG"></span>源路径


源路径指定 C 和 c + + 源文件的位置的目录。 有关在调试器中查看源的代码的详细信息，请参阅[源代码](source-code.md)。

**请注意**  如果连接到公司网络，访问源文件的最有效方法是使用源服务器。 您可以使用源服务器通过使用 srv\*源路径中的字符串。 有关源服务器的详细信息，请参阅[使用源服务器](using-a-source-server.md)。

 

若要控制在 WinDbg 中的源路径，请执行以下操作：

-   选择**Source File Path**从**文件**菜单或按 CTRL + P。

-   使用[ **.srcpath （设置源路径）** ](-srcpath---lsrcpath--set-source-path-.md)命令。 如果使用在源服务器[ **.srcfix （使用源服务器）** ](-srcfix---lsrcfix--use-source-server-.md)稍微简单一些。

-   使用[ **.lsrcpath （设置本地源路径）** ](-srcpath---lsrcpath--set-source-path-.md)命令。 如果使用在源服务器[ **.lsrcfix （使用本地源服务器）** ](-srcfix---lsrcfix--use-source-server-.md)稍微简单一些。

-   当您启动调试器时，使用 **-srcpath**或 **-lsrcpath**命令行选项。 请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

-   启动调试器之前，设置\_NT\_源\_路径[环境变量](environment-variables.md)。

## <a name="span-idopeningandclosingsourcefilesspanspan-idopeningandclosingsourcefilesspanspan-idopeningandclosingsourcefilesspanopening-and-closing-source-files"></a><span id="Opening_and_Closing_Source_Files"></span><span id="opening_and_closing_source_files"></span><span id="OPENING_AND_CLOSING_SOURCE_FILES"></span>打开和关闭源文件


若要打开或直接关闭源文件，请执行以下操作：

-   选择**打开源文件**从**文件**菜单中或按 CTRL + O。 此外可以使用**开放源代码文件**按钮 (![开放源代码文件按钮的屏幕截图](images/tbopen.png)) 工具栏上。

    **请注意**  时使用的菜单或工具栏按钮以打开源文件，该文件的路径自动追加到源路径。

     

-   选择**关闭当前窗口**从**文件**菜单。
-   单击**关闭**角的源窗口中的按钮。
-   选择**最近使用的文件**从**文件**菜单以打开一个在 WinDbg 中最近打开的四个源文件。
-   输入[ **（打开源文件） 打开**](-open--open-source-file-.md)命令。
-   输入[ **（加载或卸载源文件） 的 lsf** ](lsf--lsf---load-or-unload-source-file-.md)命令。

## <span id="ddk_source_windows_dbg"></span><span id="DDK_SOURCE_WINDOWS_DBG"></span>


在 WinDbg 中，源窗口中显示已加载到调试器的源文件。

### <a name="span-idopeningthesourcewindowspanspan-idopeningthesourcewindowspanopening-the-source-window"></a><span id="opening_the_source_window"></span><span id="OPENING_THE_SOURCE_WINDOW"></span>打开源窗口

加载新的源文件时，调试器将打开一个源窗口。 若要还原或切换到打开的源窗口，请转到**窗口**菜单和从 windows 菜单底部列表中选择。

下面的屏幕截图显示了源窗口的一个示例。

![显示已加载到调试器中的源文件的源窗口的屏幕截图](images/window-source.png)

每个源文件位于其自己的源窗口。 每个源窗口的标题是源文件的完整路径。

### <a name="span-idusingthesourcewindowspanspan-idusingthesourcewindowspanusing-the-source-window"></a><span id="using_the_source_window"></span><span id="USING_THE_SOURCE_WINDOW"></span>使用源窗口

每个源窗口将显示一个源文件的文本。 无法编辑在调试器中的源文件。 有关更改字体和选项卡上设置的详细信息，请参阅[更改文本属性](changing-text-properties.md)。

每个源窗口具有带其他命令的快捷菜单。 若要访问菜单，请右键单击标题栏或单击显示的窗口 （在右上角附近的图标![该按钮将显示源窗口工具栏上的快捷菜单的屏幕截图](images/window-source-icon.png))。 以下列表介绍了一些菜单命令：

-   **到当前行集指令指针**指令指针的值更改为与当前行相对应的指令。 此命令相当于使用[编辑 |设置当前指令](edit---set-current-instruction.md)命令或按 CTRL + SHIFT + I。

-   **编辑此文件**在文本编辑器中打开的源文件。 WinDiff 编辑器注册表信息或 WINDBG 的值确定编辑器\_INVOKE\_编辑器环境变量。 例如，考虑这种情况时的值的 WINDBG\_INVOKE\_编辑器是以下。

    ```console
    c:\my\path\myeditor.exe -file %f -line %l
    ```

    在这种情况下，Myeditor.exe 会打开到当前源文件的基于 1 的行号。 %L 选项指示数字应读取为一个基于，虽然 %f 指示应使用当前的源文件行。 其他替换可能性包括 %l，指示该行是从零开始和 %p，还可以指示应使用当前的源代码文件编号。

-   **评估所选内容**来使用 c + + 表达式计算器计算当前所选的文本。 结果出现在[调试器命令窗口](debugger-command-window.md)。 如果所选的文本中包含多个行，会产生语法错误。 此命令相当于使用[编辑 |评估所选内容](edit---evaluate-selection.md)命令，按 CTRL + SHIFT + V，或使用[ **??（计算结果 c + + 表达式）** ](----evaluate-c---expression-.md)命令作为其参数的选定文本。

-   **显示所选的类型**显示所选对象的数据类型。 调试器命令窗口中显示此显示。 如果所选的文本包括多个单个对象，可能会显示语法错误或其他异常结果。 此命令相当于使用[编辑 |显示所选类型](edit---display-selected-type.md)命令或按 CTRL + SHIFT + Y。

-   **选择打开内存窗口**将打开新的停靠的内存窗口，显示所选表达式的地址处开始的内存。

-   **将选定内容添加到监视窗口**将所选的源标记追加到监视窗口。

-   **在当前行反汇编**导致对应于当前行中显示的指令[反汇编窗口](disassembly-window.md)。 在源窗口和反汇编窗口中，突出显示所选的行，但此命令仅影响显示内容，指令指针不会更改。 如果单击此命令时，反汇编窗口已关闭，它打开。

-   **选择源语言**显示的编程语言的列表。 选择的编程语言，用于生成源代码文件，然后依次**确定**启用基本语法突出显示的当前源窗口。 选择**&lt;无&gt;** 禁用语法突出显示的当前源窗口。

### <a name="span-idsourcewindowcolorsandhoverevaluationspanspan-idsourcewindowcolorsandhoverevaluationspansource-window-colors-and-hover-evaluation"></a><span id="source_window_colors_and_hover_evaluation"></span><span id="SOURCE_WINDOW_COLORS_AND_HOVER_EVALUATION"></span>源窗口颜色和悬停评估

如果调试器识别出源文件扩展名，源窗口中显示某些语法元素的颜色。 若要关闭或更改的颜色，请执行以下操作：

-   若要在一个窗口关闭语法颜色，请打开源窗口的快捷菜单，单击**选择源语言**，然后单击 **&lt;None&gt;**。

-   若要关闭语法颜色所有源窗口，请选择**选项**从**视图**菜单。 然后清除**分析源语言**复选框。

-   若要更改语法颜色，请选择**选项**从**视图**菜单。 然后，在**颜色**区域中，选择一个语法元素，然后单击**更改**按钮更改颜色。

-   用于突出显示的分析方法由与源文件的文件扩展名相关联的编程语言确定。 若要更改与特定文件扩展名相关联的编程语言，请使用[源代码语言对话框中的文件扩展名](view---source-language-file-extensions.md)。 若要打开此对话框中，选择**源语言文件扩展名**从**视图**菜单。

表示当前的程序计数器线条将突出显示。 设置断点的行也将突出显示。

如果您选择源窗口，然后使用鼠标悬停在该窗口中的符号，将计算的符号。 计算的是与生成的相同[ **dt （显示类型）** ](dt--display-type-.md)命令。 若要停用此评估版，请选择**选项**从**视图**菜单。 然后清除**悬停时的评估**复选框。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关源调试相关的命令的详细信息，请参阅[在源模式中进行调试](debugging-in-source-mode.md)。

 

 





