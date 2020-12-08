---
title: 在 WinDbg 中查看和编辑寄存器
description: 在 WinDbg 中，可以通过输入命令、使用 "寄存器" 窗口或使用 "监视" 窗口来查看和编辑寄存器。
keywords:
- 调试信息窗口，"寄存器" 窗口
- “寄存器”窗口
- 寄存器，"寄存器" 窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e39cb18ceb9fccb47760f88c1226df1003efe282
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783459"
---
# <a name="viewing-and-editing-registers-in-windbg"></a>在 WinDbg 中查看和编辑寄存器


寄存器是位于 CPU 上的小型易失性内存单元。 许多注册专用于特定用途，其他寄存器可供用户模式应用程序使用。 基于 x86 和基于 x64 的处理器具有不同的可用寄存器集合。 有关每个处理器上寄存器的详细信息，请参阅 [处理器体系结构](processor-architecture.md)。

在 WinDbg 中，可以通过输入命令、使用 "寄存器" 窗口或使用 "监视" 窗口来查看和编辑寄存器。

## <a name="span-idcommandsspanspan-idcommandsspanspan-idcommandsspancommands"></a><span id="Commands"></span><span id="commands"></span><span id="COMMANDS"></span>命令


可以通过在调试器命令窗口中输入 [**r (寄存器)**](r--registers-.md) 命令来查看和编辑寄存器。 您可以使用多个选项或通过使用 [**rm (注册掩码)**](rm--register-mask-.md) 命令自定义显示。

每次目标停止时，也会自动显示寄存器。 如果你使用 [**p (步骤)**](p--step-.md) 或 [**t (Trace)**](t--trace-.md) 命令单步执行代码，则会看到每个步骤的寄存器显示。 若要停止此显示，请在使用这些命令时使用 **r** 选项。

在基于 x86 的处理器上， **r** 选项还控制多个称为标志的一位寄存器。 若要更改这些标志，使用的语法略有不同。 有关这些标志的详细信息以及此语法的说明，请参阅 [X86 标志](x86-architecture.md#x86-flags)。

## <a name="span-idthe_registers_windowspanspan-idthe_registers_windowspanspan-idthe_registers_windowspanthe-registers-window"></a><span id="The_Registers_Window"></span><span id="the_registers_window"></span><span id="THE_REGISTERS_WINDOW"></span>"寄存器" 窗口


### <a name="span-idopening_the_registers_windowspanspan-idopening_the_registers_windowspanspan-idopening_the_registers_windowspanopening-the-registers-window"></a><span id="Opening_the_Registers_Window"></span><span id="opening_the_registers_window"></span><span id="OPENING_THE_REGISTERS_WINDOW"></span>打开 "寄存器" 窗口

若要打开或切换到 "寄存器" 窗口，请从 "**视图**" 菜单中选择 "**注册**"。  (你还可以按 ALT + 4，或在 **Registers** ![ ](images/tbreg.png) 工具栏上) "寄存器" 按钮的屏幕截图 (选择 "注册" 按钮。 ALT + SHIFT + 4 关闭 "寄存器" 窗口。 ) 

以下屏幕截图显示了 "寄存器" 窗口的示例。

!["寄存器" 窗口的屏幕截图](images/window-registers.png)

"寄存器" 窗口包含两列。 **Reg** 列列出了目标处理器的所有寄存器。 " **值** " 列显示每个寄存器的当前值。 此窗口还包含工具栏上的 " **自定义** " 按钮，用于打开 " **自定义注册列表** " 对话框。

### <a name="span-idusing_the_registers_windowspanspan-idusing_the_registers_windowspanspan-idusing_the_registers_windowspanusing-the-registers-window"></a><span id="Using_the_Registers_Window"></span><span id="using_the_registers_window"></span><span id="USING_THE_REGISTERS_WINDOW"></span>使用 "寄存器" 窗口

在 "寄存器" 窗口中，您可以执行以下操作：

-   " **值** " 列显示每个寄存器的当前值。 最近更改的寄存器的值显示为红色文本。
    -   若要输入新值，请双击 **值** 单元，然后键入新值或编辑旧值。  ("剪切"、"复制" 和 "粘贴" 命令可用于编辑。 ) 
    -   若要保存新值，请按 ENTER。
    -   若要放弃新值，请按 ESC。
    -   如果键入的值无效，则按 ENTER 时，旧值将再次出现。
-   注册值显示在当前基数内，必须在同一基数内键入新值。 若要更改当前基数，请使用调试器命令窗口中的 [**n (Set Number Base)**](n--set-number-base-.md) 命令。

-   在用户模式下，"寄存器" 窗口显示与当前线程关联的寄存器。 有关当前线程的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

-   在内核模式下，"寄存器" 窗口显示与当前 [注册上下文](changing-contexts.md#register-context)关联的寄存器。 您可以将注册上下文设置为与特定线程、上下文记录或捕获帧匹配。 实际上只显示指定注册上下文的最重要的寄存器;不能更改其值。

"寄存器" 窗口包含一个工具栏，其中包含一个 " **自定义** " 按钮，并具有包含附加命令的快捷菜单。 若要访问菜单，请选择并按住 (右键单击标题栏) ，或选择窗口右上角附近的图标 (![ 用于显示 "寄存器" 窗口快捷) 菜单的 "按钮" 图标的屏幕截图 ](images/tbreg.png) 。 工具栏和菜单包含以下按钮和命令：

-    (工具栏和菜单) **自定义** 打开 " **自定义注册列表** " 对话框，本主题中的以下部分对此进行了说明。

-   仅 (菜单) **工具栏** 打开和关闭工具栏。

-   仅) **停靠** 或 **取消停靠 (菜单会导致** 窗口进入或离开停靠状态。

-   仅) **移动到新的停靠** (菜单关闭 "寄存器" 窗口并在新的停靠中打开它。

-   仅 (菜单) " **设置为" 窗口类型的选项卡停靠目标对于** "寄存器" 窗口不可用。 此选项仅适用于源或内存窗口。

-    ("仅) " **始终浮动** "菜单会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   仅 (菜单) **移动** 时，会导致在删除 WinDbg 帧时窗口移动，即使该窗口未停靠也是如此。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

-   仅 (菜单) **帮助** 在 Windows 调试工具文档中打开此主题。

-   仅) 关闭 (菜单 **关闭** 此窗口。

### <a name="span-idcustomize_register_list_dialog_boxspanspan-idcustomize_register_list_dialog_boxspancustomize-register-list-dialog-box"></a><span id="customize_register_list_dialog_box"></span><span id="CUSTOMIZE_REGISTER_LIST_DIALOG_BOX"></span>"自定义注册列表" 对话框

若要更改显示的寄存器列表，请选择 " **自定义** " 按钮。 将显示 " **自定义注册列表** " 对话框。

在此对话框中，您可以编辑寄存器列表，以更改寄存器的显示顺序。  (实际上不能从列表中删除寄存器;如果这样做，则会重新出现在结尾处。 ) 寄存器名称之间必须有空格。

如果选中了 " **首先显示已修改的寄存器值** " 复选框，则其值最近更改过的寄存器会出现在顶部。

如果选中 " **不显示 subregisters** " 复选框，则不会显示 subregisters。 例如，将显示 **eax** ，而不是 **ax**、 **ah** 或 **al**。

选择 **"确定"** 以保存更改，或选择 " **取消** " 放弃更改。

如果正在调试具有多种类型的处理器的多处理器计算机，则 WinDbg 分别存储每个处理器类型的自定义设置。 通过这种分离，你可以同时自定义每个处理器寄存器的显示。

## <a name="span-idddk_debugging_bios_code_dbgspanspan-idddk_debugging_bios_code_dbgspanthe-watch-window"></a><span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>"监视" 窗口


在 WinDbg 中，可以使用监视窗口显示寄存器。 不能使用监视窗口更改寄存器的值。

若要打开监视窗口，请从 "**视图**" 菜单中选择 "**监视**"。 还可以按 ALT + 2，或选择工具栏上的 **"监视" 按钮：** ![ "监视" 按钮的屏幕截图 ](images/tbwatch.png) 。 ALT + SHIFT + 2 关闭监视窗口。

下面的屏幕截图显示了一个监视窗口的示例。

!["监视" 窗口的屏幕截图 ](images/window-watch.png)

## <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关注册上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

 

 





