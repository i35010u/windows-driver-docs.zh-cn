---
title: 查看和编辑在 WinDbg 中的寄存器
description: 在 WinDbg 中，您可以查看和编辑寄存器，通过输入命令、 通过使用寄存器窗口中，或通过使用监视窗口。
ms.assetid: bd7ced3b-7f71-4ea5-a45b-38339dc3e87c
keywords:
- 调试信息窗口，寄存器窗口
- 寄存器窗口
- 寄存器，寄存器窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 434e682405af1bff8054c49c5e6c915040a5bfd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525215"
---
# <a name="viewing-and-editing-registers-in-windbg"></a>查看和编辑在 WinDbg 中的寄存器


寄存器是位于在 CPU 的小易失性内存单位。 许多寄存器专用于特定用途，并可用于用户模式应用程序使用的其他寄存器。 基于 x86 和基于 x64 的处理器在有可用的寄存器的不同集合。 在每个处理器寄存器的详细信息，请参阅[处理器体系结构](processor-architecture.md)。

在 WinDbg 中，您可以查看和编辑寄存器，通过输入命令、 通过使用寄存器窗口中，或通过使用监视窗口。

## <a name="span-idcommandsspanspan-idcommandsspanspan-idcommandsspancommands"></a><span id="Commands"></span><span id="commands"></span><span id="COMMANDS"></span>命令


你可以查看和编辑通过输入的寄存器[ **r （寄存器）** ](r--registers-.md)命令在调试器命令窗口中。 可以使用多个选项或使用自定义显示[ **rm （注册掩码）** ](rm--register-mask-.md)命令。

寄存器也会自动显示每个目标停止的时间。 如果在逐句通过代码[ **p （步骤）** ](p--step-.md)或[ **t (Trace)** ](t--trace-.md)命令，你将看到一个函数注册表，显示每个步骤。 若要停止此显示，请使用**r**选项时使用这些命令。

在基于 x86 的处理器上， **r**选项还可以控制多个名为标志的一位寄存器。 若要更改这些标志，您可以使用比时更改常规寄存器略有不同的语法。 有关这些标志和此语法的说明的详细信息，请参阅[x86 标志](x86-architecture.md#x86-flags)。

## <a name="span-idtheregisterswindowspanspan-idtheregisterswindowspanspan-idtheregisterswindowspanthe-registers-window"></a><span id="The_Registers_Window"></span><span id="the_registers_window"></span><span id="THE_REGISTERS_WINDOW"></span>寄存器窗口


### <a name="span-idopeningtheregisterswindowspanspan-idopeningtheregisterswindowspanspan-idopeningtheregisterswindowspanopening-the-registers-window"></a><span id="Opening_the_Registers_Window"></span><span id="opening_the_registers_window"></span><span id="OPENING_THE_REGISTERS_WINDOW"></span>打开寄存器窗口

若要打开或切换到寄存器窗口，请选择**注册**从**视图**菜单。 (还可以按 ALT + 4，或单击**注册**按钮 (![寄存器按钮的屏幕截图](images/tbreg.png)) 工具栏上。 ALT + SHIFT + 4 关闭寄存器窗口。）

以下屏幕截图显示寄存器窗口的示例。

![寄存器窗口的屏幕截图](images/window-registers.png)

寄存器窗口包含两个列。 **Reg**列列出了所有目标处理器的寄存器。 **值**列显示每个注册的当前值。 此窗口还包含**自定义**按钮在工具栏上，打开**自定义注册列表**对话框。

### <a name="span-idusingtheregisterswindowspanspan-idusingtheregisterswindowspanspan-idusingtheregisterswindowspanusing-the-registers-window"></a><span id="Using_the_Registers_Window"></span><span id="using_the_registers_window"></span><span id="USING_THE_REGISTERS_WINDOW"></span>使用寄存器窗口

在寄存器窗口中，可以执行以下操作：

-   **值**列显示每个注册的当前值。 以红色文本显示的最近更改的寄存器的值。
    -   若要输入新值，请双击**值**单元格，然后键入新值或编辑旧值。 （剪切、 复制和粘贴命令是可用来进行编辑。）
    -   若要保存新值，请按 ENTER。
    -   若要放弃的新值，请按 ESC。
    -   如果键入无效的值，按 ENTER 键时，将重新出现的旧值。
-   寄存器值显示在当前的基数，并且必须在相同的基数中键入新值。 若要更改当前的基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令在调试器命令窗口中。

-   在用户模式下，寄存器窗口显示与当前线程相关联的寄存器。 有关当前线程的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

-   在内核模式下，寄存器窗口显示与当前相关联的寄存器[注册上下文](changing-contexts.md#register-context)。 可以设置寄存器上下文以匹配特定线程、 上下文记录或捕获帧。 实际显示仅指定的寄存器上下文的最重要寄存器;不能更改它们的值。

寄存器窗口已包含一个工具栏**自定义**按钮和具有带其他命令的快捷菜单。 若要访问菜单，请右键单击标题栏或单击窗口右上角附近的图标 (![用于显示寄存器窗口快捷菜单的按钮图标的屏幕截图](images/tbreg.png))。 工具栏和菜单包含以下按钮和命令：

-   （工具栏和菜单）**自定义**会打开**自定义注册列表**对话框中，在本主题中的以下部分中所述。

-   （仅限菜单）**工具栏**工具栏，开启和关闭。

-   （仅限菜单）**停靠**或**取消停靠**将使窗口进入或离开停靠的状态。

-   （仅限菜单）**移到新停靠**寄存器窗口将关闭，并将其打开新的平台中。

-   （仅限菜单）**设置为选项卡形式停靠为窗口中，键入目标**不可用于寄存器窗口。 此选项才可用的源或内存窗口。

-   （仅限菜单）**始终浮点**将使窗口停靠，即使仍拖到停靠位置。

-   （仅限菜单）**移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。

-   （仅限菜单）**帮助**有关 Windows 调试工具文档中打开此主题。

-   （仅限菜单）**关闭**关闭此窗口。

### <a name="span-idcustomizeregisterlistdialogboxspanspan-idcustomizeregisterlistdialogboxspancustomize-register-list-dialog-box"></a><span id="customize_register_list_dialog_box"></span><span id="CUSTOMIZE_REGISTER_LIST_DIALOG_BOX"></span>自定义注册列表对话框

若要更改显示的寄存器的列表，请单击**自定义**按钮。 **自定义注册列表**对话框将出现。

在此对话框中，可以编辑的寄存器，若要更改的寄存器的显示的顺序的列表。 （不能实际从列表中删除注册; 如果这样做，它将结束时重新出现。）注册名称之间必须留一个空格。

如果选择**修改显示首次注册值**复选框，其值已更改的寄存器最近显示在顶部。

如果选择**不会显示 subregisters**复选框，subregisters 不会显示。 例如， **eax**将显示，但不是**ax**， **ah**，或者**al**。

单击**确定**以保存所做的更改或**取消**放弃所做的更改。

如果你正在调试多个类型的处理器的多处理器计算机，WinDbg 将单独存储每个处理器类型的自定义设置。 这种分离使您可以同时自定义的每个处理器的寄存器的显示。

## <a name="span-idddkdebuggingbioscodedbgspanspan-idddkdebuggingbioscodedbgspanthe-watch-window"></a><span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>监视窗口


在 WinDbg 中，可以使用监视窗口显示寄存器。 不能使用监视窗口更改的寄存器的值。

若要打开监视窗口，请选择**Watch**从**视图**菜单。 此外可以按 ALT + 2，或单击**Watch**工具栏上的按钮：![监视按钮的屏幕截图](images/tbwatch.png)。 ALT + SHIFT + 2 将关闭监视窗口。

下面的屏幕截图显示了监视窗口的示例。

![监视窗口的屏幕截图 ](images/window-watch.png)

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关寄存器上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

 

 





