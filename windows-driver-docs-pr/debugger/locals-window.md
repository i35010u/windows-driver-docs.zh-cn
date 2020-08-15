---
title: 在 WinDbg 中查看和编辑局部变量
description: 在 WinDbg 中，可以通过输入命令、使用 "局部变量" 窗口或使用监视窗口来查看局部变量。
ms.assetid: 9d816df7-2b20-4be3-90d7-7a11b0f30238
keywords:
- 调试信息窗口，本地窗口
- 局部变量窗口
- 内存，局部变量窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a77bd8cee247602254c8be3f949bc64f55efe0e3
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252905"
---
# <a name="viewing-and-editing-local-variables-in-windbg"></a>在 WinDbg 中查看和编辑局部变量


在 WinDbg 中，可以通过输入命令、使用 "局部变量" 窗口或使用监视窗口来查看局部变量。

## <a name="span-iddebugger_command_windowspanspan-iddebugger_command_windowspanspan-iddebugger_command_windowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


您可以通过在调试器命令窗口中输入 [**dv**](dv--display-local-variables-.md) 命令或 [**dt**](dt--display-type-.md) 命令来查看局部变量和参数。

## <a name="span-idddk_locals_window_dbgspanspan-idddk_locals_window_dbgspanopening-the-locals-window"></a><span id="ddk_locals_window_dbg"></span><span id="DDK_LOCALS_WINDOW_DBG"></span>打开 "局部变量" 窗口


"局部变量" 窗口显示有关当前范围内的所有本地变量的信息。

若要打开或切换到 "局部变量" 窗口，请在 "WinDbg" 窗口的 " **视图** " 菜单上，选择 " **局部变量**"。  (还可以按 ALT + 3，或在**Locals** ![ ](images/tblocal.png) 工具栏上的 "局部变量" 按钮)  (屏幕截图中选择 "局部变量" 按钮。 ALT + SHIFT + 3 关闭 "局部变量" 窗口。 ) 

以下屏幕截图显示了一个 "局部变量" 窗口的示例。

!["局部变量" 窗口的屏幕截图 ](images/window-locals.png)

"局部变量" 窗口可以包含四列。 " **名称** " 和 " **值** " 列始终显示，" **类型** " 和 " **位置** " 列是可选的。 若要显示 " **类型** " 和 " **位置** " 列，请分别在工具栏上选择 " **转换** " 和 " **位置** " 按钮。

## <a name="span-idusing_the_locals_windowspanspan-idusing_the_locals_windowspanspan-idusing_the_locals_windowspanusing-the-locals-window"></a><span id="Using_the_Locals_Window"></span><span id="using_the_locals_window"></span><span id="USING_THE_LOCALS_WINDOW"></span>使用 "局部变量" 窗口


在 "局部变量" 窗口中，您可以执行以下操作：

-   " **名称** " 列显示每个局部变量的名称。 如果变量是数据结构，则其名称旁边会出现一个复选框。 若要展开或折叠结构成员的显示，请选中或清除相应的复选框。

-   " **值** " 列显示每个变量的当前值。

    -   若要为变量输入新值，请双击当前值并键入新值，或编辑旧值。  ("剪切"、"复制" 和 "粘贴" 命令可用于编辑。 ) 可以键入任何 [c + + 表达式](c---numbers-and-operators.md)。
    -   若要保存新值，请按 ENTER。
    -   若要放弃新值，请按 ESC。
    -   如果键入的值无效，则按 ENTER 时，旧值将再次出现。

    **Int**类型的整数显示为十进制值;**UINT**类型的整数显示在当前基数中。 若要更改当前基数，请使用调试器命令窗口中的 [**n (Set Number Base) **](n--set-number-base-.md) 命令。

-   如果 "类型" 列显示在 "局部变量" 窗口中，则该 **类型** 列 () 显示每个变量的当前数据类型。 每个变量显示为其自身数据类型的正确格式。 数据结构的类型名称在 **类型** 列中。 其他变量类型在此列中显示 "输入新类型"。

    如果双击 "输入新类型"，则可以通过输入新数据类型来强制转换类型。 此强制转换仅在 "局部变量" 窗口中更改此变量的当前显示。它不会更改调试器或目标计算机上的任何内容。 此外，如果在 " **值** " 列中输入新值，则将根据符号的实际类型（而不是您在 " **类型** " 列中输入的任何新类型）来分析输入的文本。 如果关闭再重新打开 "局部变量" 窗口，则会丢失数据类型更改。

    您还可以在 " **类型** " 列中输入扩展命令。 调试器会将符号地址传递到此扩展，并将生成的输出显示在当前行下一系列可折叠行中。 例如，如果此行中的符号是线程环境块的有效地址，则可以在 "**类型**" 列中输入 **！ teb** ，在该符号的地址上运行[**！ teb**](-teb.md)扩展。

-   " **位置** " 列 (显示在 "局部变量" 窗口中，) 显示数据结构中每个成员的偏移量。

-   如果本地变量是包含 Vtables 的类的实例，则 **Name** 列将显示 Vtables，你可以展开 Vtables 以显示函数指针。 如果 Vtable 包含在指向派生实现的基类中，则会显示 notation ** \_ vtcast \_ 类**，以指示由于派生类而添加的成员。 这些成员扩展为派生类类型。

-   [本地上下文](changing-contexts.md#local-context)决定将在 "局部变量" 窗口中显示的本地变量集。 由于任何原因本地上下文发生变化时，将自动更新 "局部变量" 窗口。 默认情况下，本地上下文与程序计数器的当前位置匹配。 有关如何更改本地上下文的详细信息，请参阅本地上下文。

"局部变量" 窗口包含一个工具栏，其中包含两个按钮 (**转换** 和 **位置**) ，还有一个包含附加命令的快捷菜单。 若要访问菜单，请选择并按住 (或右键单击窗口的标题栏) ，或选择窗口右上角附近的图标 (![ 本主题中的两个按钮图标是相同的，但似乎为不同的函数提供了 ](images/window-locals-menu-icon.png)) 。 工具栏和菜单包含以下按钮和命令：

-    (工具栏和菜单) **转换** 打开和关闭 **类型** 列的显示。

-    (工具栏和菜单) **位置** 将打开和关闭 **Location** 列的显示。

-    (菜单仅) **显示16位值，因为 unicode** 在此窗口中显示 unicode 字符串。 此命令打开和关闭影响 "局部变量" 窗口、"监视窗口" 和 "调试器" 命令输出的全局设置。 此命令等效于使用 [**. enable \_ Unicode (Enable unicode Display) **](-enable-unicode--enable-unicode-display-.md) 命令。

-    (菜单仅) **始终在默认基数中显示数字** 会导致整数以默认基数显示，而不是以十进制格式显示。 此命令打开和关闭影响 "局部变量" 窗口、"监视窗口" 和 "调试器" 命令输出的全局设置。 此命令等效于使用 [**. force \_ 基数 \_ 输出 (对整数使用基数) **](-force-radix-output--use-radix-for-integers-.md) 命令。

    **注意**   "**始终在默认基数中显示数字**" 命令不会影响长整数。 长整数以十进制格式显示，除非 [**. 启用 \_ 长 \_ 整型状态 (启用长整数显示) **](-enable-long-status--enable-long-integer-display-.md) 命令设置。 **. 启用 \_ 长 \_ 状态**命令会影响在 "局部变量" 窗口、"监视窗口" 和 "调试器" 命令输出中的显示; 在 "局部变量" 窗口的菜单中不存在与此命令等效的等效项。

     

-    (菜单 "仅) **所选值的" 打开内存 "窗口** 打开一个新的停靠内存窗口，该窗口显示从所选表达式的地址开始的内存。

-   仅 (菜单) **为所选内存值调用 dt** 会运行 [**Dt (显示类型) **](dt--display-type-.md) 命令，并将所选符号作为其参数。 结果将显示在调试器命令窗口中。 自动使用 **-n** 选项来区分十六进制地址中的符号。 不使用其他选项。 请注意，使用此菜单选项生成的内容与从命令行运行 **dt** 命令时生成的内容相同，但格式略有不同。

-   仅 (菜单) **工具栏** 打开和关闭工具栏。

-   仅) **停靠** 或 **取消停靠 (菜单会导致** 窗口进入或离开停靠状态。

-   仅) **移动到新的停靠** (菜单关闭 "局部变量" 窗口，并在新的停靠中打开它。

-   仅 (菜单) " **设置为" 窗口类型的选项卡停靠目标对于** "局部变量" 窗口不可用。 此选项仅适用于源或内存窗口。

-    ("仅) " **始终浮动** "菜单会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   仅 (菜单) **移动** 时，会导致在删除 WinDbg 帧时窗口移动，即使该窗口未停靠也是如此。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

-   仅 (菜单) **帮助** 在 Windows 调试工具文档中打开此主题。

-   仅) 关闭 (菜单 **关闭** 此窗口。

## <a name="span-idddk_debugging_bios_code_dbgspanspan-idddk_debugging_bios_code_dbgspanthe-watch-window"></a><span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>"监视" 窗口


在 WinDbg 中，可以使用监视窗口显示和更改局部变量。 监视窗口可以显示所需的任何变量列表。 这些变量可以包含来自任何函数的全局变量和局部变量。 在任何时候，监视窗口都将显示与当前函数的作用域匹配的那些变量的值。 还可以通过监视窗口更改这些变量的值。

与 "局部变量" 窗口不同，监视窗口不受本地上下文更改的影响。 只有在当前程序计数器的作用域中定义的那些变量才能显示或修改其值。

若要打开监视窗口，请从 "**视图**" 菜单中选择 "**监视**"。 还可以按 ALT + 2，或选择工具栏上的 **"监视" 按钮：** ![ "监视" 按钮的屏幕截图 ](images/tbwatch.png) 。 ALT + SHIFT + 2 关闭监视窗口。

下面的屏幕截图显示了一个监视窗口的示例。

!["监视" 窗口的屏幕截图 ](images/window-watch.png)

监视窗口可以包含四列。 " **名称** " 和 " **值** " 列始终显示，" **类型** " 和 " **位置** " 列是可选的。 若要显示 " **类型** " 和 " **位置** " 列，请分别在工具栏上选择 " **转换** " 和 " **位置** " 按钮。

## <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关控制局部变量的详细信息，请参阅使用变量和更改范围，以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

 

 





