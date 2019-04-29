---
title: 在 WinDbg 中查看和编辑局部变量
description: 在 WinDbg 中，输入命令，使用局部变量窗口中，或使用监视窗口可以查看本地变量。
ms.assetid: 9d816df7-2b20-4be3-90d7-7a11b0f30238
keywords:
- 调试信息窗口中，局部变量窗口
- 局部变量窗口
- 内存中，局部变量窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4a637edb0b15d7246758585ac172feb6d221def
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383468"
---
# <a name="viewing-and-editing-local-variables-in-windbg"></a>在 WinDbg 中查看和编辑局部变量


在 WinDbg 中，输入命令，使用局部变量窗口中，或使用监视窗口可以查看本地变量。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


可以通过输入查看本地变量和参数[ **dv** ](dv--display-local-variables-.md)命令或[ **dt** ](dt--display-type-.md)命令在调试器命令窗口中。

## <a name="span-idddklocalswindowdbgspanspan-idddklocalswindowdbgspanopening-the-locals-window"></a><span id="ddk_locals_window_dbg"></span><span id="DDK_LOCALS_WINDOW_DBG"></span>打开局部变量窗口


局部变量窗口显示当前作用域中的本地变量的所有信息。

若要打开或切换到局部变量窗口中，在 WinDbg 窗口中，在**视图**菜单上，单击**局部变量**。 (还可以按 ALT + 3，或单击**局部变量**按钮 (![局部变量按钮的屏幕截图](images/tblocal.png)) 工具栏上。 ALT + SHIFT + 3 关闭局部变量窗口。）

下面的屏幕截图显示了局部变量窗口的一个示例。

![局部变量窗口的屏幕截图 ](images/window-locals.png)

局部变量窗口可以包含四个列。 **名称**并**值**始终显示列，并**类型**并**位置**列是可选的。 若要显示**类型**并**位置**列，单击**Typecast**并**位置**按钮，分别在工具栏上。

## <a name="span-idusingthelocalswindowspanspan-idusingthelocalswindowspanspan-idusingthelocalswindowspanusing-the-locals-window"></a><span id="Using_the_Locals_Window"></span><span id="using_the_locals_window"></span><span id="USING_THE_LOCALS_WINDOW"></span>使用局部变量窗口


在局部变量窗口中，可以执行以下操作：

-   **名称**列显示每个本地变量的名称。 如果变量是一种数据结构，其名称旁边显示复选框。 若要展开或折叠结构成员的显示，请选择或清除该复选框。

-   **值**列显示每个变量的当前值。

    -   若要为变量输入新值，双击当前值并键入新值，或编辑旧值。 （剪切、 复制和粘贴命令是可用来进行编辑。）您可以键入任何[C++表达式](c---numbers-and-operators.md)。
    -   若要保存新值，请按 ENTER。
    -   若要放弃的新值，请按 ESC。
    -   如果键入无效的值，按 ENTER 键时，将重新出现的旧值。

    类型的整数**int**显示为十进制值; 类型的整数**UINT**显示在当前的基数。 若要更改当前的基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令在调试器命令窗口中。

-   **类型**列 （如果它显示在局部变量窗口中） 显示每个变量的当前数据类型。 每个变量显示在其自己的数据类型为正确的格式。 数据结构具有其类型名**类型**列。 其他变量的类型显示在此列中的"输入新的类型"。

    如果您双击"输入新类型"，您可以通过输入新的数据类型强制转换类型。 此强制转换更改仅在局部变量窗口中; 此变量的当前显示它不会更改任何内容在调试器中或在目标计算机上。 此外，如果输入中的新值**值**列中，你输入的文本将分析基于符号的实际类型而不是任何新型中输入**类型**列。 如果关闭并重新打开局部变量窗口，您将丢失的数据类型更改。

    您还可以输入中的扩展命令**类型**列。 调试器会将该符号的地址传递到此扩展插件，并将在一系列的当前行下方的可折叠行中显示生成的输出。 例如，如果在此行中的符号是有效的线程环境块的地址，则可以输入 **！ teb**中**类型**列来运行[ **！ teb** ](-teb.md)此符号的地址上的扩展。

-   **位置**列 （如果它显示在局部变量窗口中） 显示了一种数据结构的每个成员的偏移量。

-   如果本地变量是一个包含 Vtable，类的实例**名称**列显示 Vtable，并且可以扩展 Vtable 以显示函数指针。 如果在指向派生的实现，表示法的基类中包含 Vtable  **\_vtcast\_类**显示来指示添加，则由于派生类的成员。 这些成员展开类似于派生的类类型。

-   [本地上下文](changing-contexts.md#local-context)确定哪些组的本地变量将显示在局部变量窗口。 当本地上下文的任何原因发生更改时，会自动更新局部变量窗口。 默认情况下，本地上下文与匹配程序计数器的当前位置。 有关如何更改本地上下文的详细信息，请参阅本地上下文。

局部变量窗口有一个包含两个按钮的工具栏 (**Typecast**并**位置**) 以及一个具有其他命令的快捷菜单。 若要访问菜单，请右键单击该窗口的标题栏或单击窗口右上角附近的图标 (![的两个按钮本主题中的图标相同，但它们看起来具有不同职责](images/window-locals-menu-icon.png))。 工具栏和菜单包含以下按钮和命令：

-   （工具栏和菜单）**Typecast**将显示**类型**列打开和关闭。

-   （工具栏和菜单）**位置**将显示**位置**列打开和关闭。

-   （仅限菜单）**显示 16 位值作为 Unicode**此窗口中显示的 Unicode 字符串。 此命令将打开和关闭全局设置，它会影响局部变量窗口、 监视窗口和调试器命令输出。 此命令相当于使用[ **.enable\_unicode （启用 Unicode 显示器）** ](-enable-unicode--enable-unicode-display-.md)命令。

-   （仅限菜单）**始终显示在默认数字基数**导致要在显示中而不是以十进制格式显示它们的默认基数的整数。 此命令将打开和关闭全局设置，它会影响局部变量窗口、 监视窗口和调试器命令输出。 此命令相当于使用[ **.force\_基数\_输出 （使用基数范围内的整数）** ](-force-radix-output--use-radix-for-integers-.md)命令。

    **请注意**   **始终显示在默认数字基数**命令不会影响长整数。 除非以十进制格式显示长整数[ **.enable\_长\_状态 （启用长整数的显示）** ](-enable-long-status--enable-long-integer-display-.md)命令集。 **.Enable\_长\_状态**命令会影响显示在局部变量窗口中，监视窗口和调试器命令输出中; 没有为此命令在局部变量窗口中的菜单中没有等效项。

     

-   （仅限菜单）**选定的值为打开内存窗口**将打开新的停靠的内存窗口，显示所选表达式的地址处开始的内存。

-   （仅限菜单）**调用所选的内存值的 dt**运行[ **dt （显示类型）** ](dt--display-type-.md)命令与所选符号作为其参数。 调试器命令窗口中显示结果。 **-N**选项自动用于将符号与十六进制地址区分开来。 未不使用任何其他选项。 请注意，使用此菜单选项生成的内容是与运行时生成的内容相同**dt**命令从命令行中，但格式会略有不同。

-   （仅限菜单）**工具栏**工具栏，开启和关闭。

-   （仅限菜单）**停靠**或**取消停靠**将使窗口进入或离开停靠的状态。

-   （仅限菜单）**移到新停靠**局部变量窗口将关闭，并将其打开新的平台中。

-   （仅限菜单）**设置为选项卡形式停靠为窗口中，键入目标**局部变量窗口不可用。 此选项才可用的源或内存窗口。

-   （仅限菜单）**始终浮点**将使窗口停靠，即使仍拖到停靠位置。

-   （仅限菜单）**移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。

-   （仅限菜单）**帮助**有关 Windows 调试工具文档中打开此主题。

-   （仅限菜单）**关闭**关闭此窗口。

## <a name="span-idddkdebuggingbioscodedbgspanspan-idddkdebuggingbioscodedbgspanthe-watch-window"></a><span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>监视窗口


在 WinDbg 中，可以使用监视窗口可显示和更改本地变量。 监视窗口可以显示任何所需的变量的列表。 这些变量可以包含全局变量和局部变量从任何函数。 在任何时候，监视窗口显示与当前函数的作用域匹配这些变量的值。 此外可以更改通过监视窗口的这些变量的值。

与局部变量窗口中，监视窗口不受对本地上下文的更改。 当前的程序计数器的作用域中定义的变量可以具有其值显示或修改。

若要打开监视窗口，请选择**Watch**从**视图**菜单。 此外可以按 ALT + 2，或单击**Watch**工具栏上的按钮：![监视按钮的屏幕截图](images/tbwatch.png)。 ALT + SHIFT + 2 将关闭监视窗口。

下面的屏幕截图显示了监视窗口的示例。

![监视窗口的屏幕截图 ](images/window-watch.png)

监视窗口可以包含四个列。 **名称**并**值**始终显示列，并**类型**并**位置**列是可选的。 若要显示**类型**并**位置**列，单击**Typecast**并**位置**按钮，分别在工具栏上。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关控制本地变量的详细信息，请参阅使用变量和更改作用域和其他与内存相关的命令，说明的概述[读取和写入内存](reading-and-writing-memory.md)。

 

 





