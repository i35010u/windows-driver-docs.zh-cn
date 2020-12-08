---
title: 在 WinDbg 中进行源代码调试
description: 在 WinDbg 中进行源代码调试
keywords:
- 调试信息窗口，源窗口
- 源窗口
- 源调试，源窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65def7311476a24d91440282b9fd0f6743878df6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791619"
---
# <a name="source-code-debugging-in-windbg"></a>在 WinDbg 中进行源代码调试


## <a name="span-idddk_source_path_dbgspanspan-idddk_source_path_dbgspansource-path"></a><span id="ddk_source_path_dbg"></span><span id="DDK_SOURCE_PATH_DBG"></span>源路径


源路径指定 C 和 c + + 源文件所在的目录。 有关在调试器中查看源代码的详细信息，请参阅 [源代码](source-code.md)。

**注意**   如果已连接到公司网络，则访问源文件的最有效方法是使用源服务器。 您可以通过使用源路径中的 srv 字符串来使用源服务器 \* 。 有关源服务器的详细信息，请参阅 [使用源服务器](using-a-source-server.md)。

 

若要在 WinDbg 中控制源路径，请执行以下操作之一：

-   从 "**文件**" 菜单中选择 "**源文件路径**" 或按 CTRL + P。

-   使用 [**. srcpath (设置源路径)**](-srcpath---lsrcpath--set-source-path-.md) 命令。 如果使用源服务器，则 [**srcfix (使用源服务器)**](-srcfix---lsrcfix--use-source-server-.md) 会稍微简单一些。

-   使用 [**. lsrcpath (设置本地源路径)**](-srcpath---lsrcpath--set-source-path-.md) 命令。 如果使用源服务器，则 [**lsrcfix (使用本地源服务器)**](-srcfix---lsrcfix--use-source-server-.md) 会稍微简单一些。

-   启动调试器时，请使用 **-srcpath** 或 **-lsrcpath** 命令行选项。 请参阅 [**WinDbg Command-Line 选项**](windbg-command-line-options.md)。

-   在启动调试器之前，请设置 \_ NT \_ 源 \_ 路径 [环境变量](environment-variables.md)。

## <a name="span-idopening_and_closing_source_filesspanspan-idopening_and_closing_source_filesspanspan-idopening_and_closing_source_filesspanopening-and-closing-source-files"></a><span id="Opening_and_Closing_Source_Files"></span><span id="opening_and_closing_source_files"></span><span id="OPENING_AND_CLOSING_SOURCE_FILES"></span>打开和关闭源文件


若要直接打开或关闭源文件，请执行下列操作之一：

-   从 "**文件**" 菜单中选择 "**打开源文件**"，或按 CTRL + O。 你还可以使用 " **打开源文件** " 按钮 (![ 工具栏上的 "打开源文件" 按钮 ](images/tbopen.png)) 屏幕截图。

    **注意**  使用菜单或工具栏按钮打开源文件时，该文件的路径会自动追加到源路径。

     

-   从 "**文件**" 菜单中选择 "**关闭当前窗口**"。
-   选择源窗口角的 " **关闭** " 按钮。
-   从 "**文件**" 菜单中选择 "**最近使用的文件**" 以打开在 WinDbg 中最近打开的四个源文件之一。
-   输入 [**(Open Source File)**](-open--open-source-file-.md) 命令。
-   输入 [**lsf (加载或卸载源文件)**](lsf--lsf---load-or-unload-source-file-.md) 命令。

## <span id="ddk_source_windows_dbg"></span><span id="DDK_SOURCE_WINDOWS_DBG"></span>


在 WinDbg 中，源窗口显示已加载到调试器中的源文件。

### <a name="span-idopening_the_source_windowspanspan-idopening_the_source_windowspanopening-the-source-window"></a><span id="opening_the_source_window"></span><span id="OPENING_THE_SOURCE_WINDOW"></span>打开源窗口

调试器在加载新源文件时打开一个源窗口。 若要还原或切换到打开的源窗口，请转到 " **窗口** " 菜单并从菜单底部的窗口列表中进行选择。

下面的屏幕截图显示源窗口的示例。

![源窗口的屏幕截图，显示已加载到调试器中的源文件](images/window-source.png)

每个源文件都位于其自己的源窗口中。 每个源窗口的标题是源文件的完整路径。

### <a name="span-idusing_the_source_windowspanspan-idusing_the_source_windowspanusing-the-source-window"></a><span id="using_the_source_window"></span><span id="USING_THE_SOURCE_WINDOW"></span>使用源窗口

每个源窗口都显示一个源文件的文本。 不能在调试器中编辑源文件。 有关更改字体和选项卡设置的详细信息，请参阅 [更改文本属性](changing-text-properties.md)。

每个源窗口都具有包含附加命令的快捷菜单。 若要访问菜单，请选择并按住 (或右键单击标题栏) 或选择出现在窗口右上角附近的图标 (![显示源窗口工具栏快捷菜单的按钮屏幕截图](images/window-source-icon.png)). 以下列表描述了一些菜单命令：

-   **将指令指针设置为当前行** 会将指令指针的值更改为对应于当前行的指令。 此命令等效于使用 " [编辑 |设置当前指令](edit---set-current-instruction.md) 命令或按 CTRL + SHIFT + I。

-   **编辑此文件** 将在文本编辑器中打开源文件。 编辑器由 WinDiff 编辑器注册表信息或 WINDBG \_ 调用 \_ 编辑器环境变量的值确定。 例如，假设 WINDBG \_ 调用编辑器的值 \_ 如下所示。

    ```console
    c:\my\path\myeditor.exe -file %f -line %l
    ```

    在这种情况下，Myeditor.exe 将打开当前源文件的从1开始的行号。 % L 选项指示行号应作为一开始读取，而% f 指示应使用当前源文件。 其他替换可能性包括：% L，这表示行号从零开始，% p 还可能指示应使用当前源文件。

-   **计算选择** 通过使用 c + + 表达式计算器来计算当前选定的文本。 结果将显示在 [调试器命令窗口](debugger-command-window.md)中。 如果所选文本包含多行，则会产生语法错误。 此命令等效于使用 " [编辑 |计算选择](edit---evaluate-selection.md) 命令，按 CTRL + SHIFT + V，或使用 "？" (使用所选文本作为参数来 [**计算 c + + 表达式)**](----evaluate-c---expression-.md) 命令。

-   **显示选定的类型** 显示所选对象的数据类型。 此显示显示在调试器命令窗口中。 如果所选文本包含多个对象，则可能会显示语法错误或其他不稳定的结果。 此命令等效于使用 " [编辑 |显示选定的类型](edit---display-selected-type.md) 命令，或按 CTRL + SHIFT + Y。

-   **用于选择的 "打开内存" 窗口** 打开一个新的停靠内存窗口，该窗口显示从所选表达式的地址开始的内存。

-   **将所选内容添加到监视窗口** 将所选源令牌追加到监视窗口中。

-   **当前行的拆装** 会导致与当前行对应的指令出现在 "反汇编" [窗口](disassembly-window.md)中。 选定的行将在源窗口和 "反汇编" 窗口中突出显示，但此命令仅影响显示，而不会更改指令指针。 如果在选择该命令时 "反汇编" 窗口关闭，则将其打开。

-   **选择源语言** 显示一系列编程语言。 选择用于生成源文件的编程语言，然后选择 **"确定"** 以为当前源窗口启用基本语法突出显示。 选择 " **&lt; 无 &gt;** " 可对当前源窗口禁用语法突出显示。

### <a name="span-idsource_window_colors_and_hover_evaluationspanspan-idsource_window_colors_and_hover_evaluationspansource-window-colors-and-hover-evaluation"></a><span id="source_window_colors_and_hover_evaluation"></span><span id="SOURCE_WINDOW_COLORS_AND_HOVER_EVALUATION"></span>源窗口颜色和悬停计算

如果调试器识别源文件扩展名，则源窗口将以彩色显示某些语法元素。 若要关闭或更改颜色，请执行以下操作：

-   若要在单个窗口中关闭语法颜色，请打开源窗口的快捷菜单，选择 "**选择源语言**"，然后选择 " **&lt; &gt; 无**"。

-   若要为所有源窗口关闭语法颜色，请从 "**视图**" 菜单中选择 "**选项**"。 然后清除 " **分析源语言** " 复选框。

-   若要更改语法颜色，请从 "**视图**" 菜单中选择 "**选项**"。 然后，在 " **颜色** " 区域中，选择一个语法元素，然后选择 " **更改** " 按钮以更改颜色。

-   用于突出显示的分析方法取决于与源文件的文件扩展名相关联的编程语言。 若要更改与特定文件扩展名关联的编程语言，请使用 " [源语言的文件扩展名" 对话框](view---source-language-file-extensions.md)。 若要打开此对话框，请在 "**视图**" 菜单中选择 "**源语言文件扩展名**"。

突出显示表示当前程序计数器的行。 还将突出显示断点所在的行。

如果选择源窗口，然后使用鼠标将鼠标悬停在该窗口中的某个符号上，则将对该符号进行计算。 此计算与 [**dt (显示类型)**](dt--display-type-.md) 命令生成的值相同。 若要停用此评估，请从 "**视图**" 菜单中选择 "**选项**"。 然后清除 " **悬停时计算** " 复选框。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关源调试和相关命令的详细信息，请参阅 [源模式下的调试](debugging-in-source-mode.md)。

 

 





