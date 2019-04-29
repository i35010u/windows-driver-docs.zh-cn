---
title: 在 WinDbg 中进行程序集代码调试
description: 在 WinDbg 中，您可以通过输入命令或通过使用反汇编窗口查看程序集代码。
ms.assetid: e00ea29e-4153-4588-8353-de69910bfc65
keywords:
- 调试信息窗口中，反汇编窗口
- 反汇编窗口
- 调试时，反汇编窗口的程序集
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0a6a42777178a219cc1b47a85aed07bb520e1a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363985"
---
# <a name="assembly-code-debugging-in-windbg"></a>在 WinDbg 中进行程序集代码调试


在 WinDbg 中，您可以通过输入命令或通过使用反汇编窗口查看程序集代码。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


可以通过输入之一查看程序集代码[ **u，ub，uu （反汇编）** ](u--unassemble-.md)调试器命令窗口中的命令。

## <a name="span-idddkdisassemblywindowdbgspanspan-idddkdisassemblywindowdbgspandissasembly-window"></a><span id="ddk_disassembly_window_dbg"></span><span id="DDK_DISASSEMBLY_WINDOW_DBG"></span>Dissasembly 窗口


若要打开或切换到反汇编窗口时，选择**Dissasembly**从**视图**菜单。 (还可以按 ALT + 7，或单击**反汇编**按钮 (![反汇编按钮的屏幕截图](images/tbdisasm2.png)) 工具栏上。 ALT + SHIFT + 7 将关闭反汇编窗口。）

以下屏幕截图显示反汇编窗口的一个示例。

![反汇编窗口的屏幕截图](images/window-disassembly.png)

调试器采用一段的内存，将其解释为二进制的机器指令，然后反汇编应用程序生成的机器指令的程序集语言版本。 生成的代码显示在反汇编窗口中。

在反汇编窗口中，可以执行以下操作：

-   在反汇编内存的其他部分**偏移量**框中，键入你想要拆装的内存的地址。 （您可以键入地址，后面按 ENTER，但您没有到。）反汇编窗口显示代码之前已完成地址;你可以忽略此代码。

-   若要查看内存的其他部分，单击**上一步**或**下一步**按钮或按 PAGE UP 或 PAGE DOWN 键。 这些命令将分别显示的内存，前面或后面的部分中的反汇编的代码。 通过按向右键、 向左键、 向上键和向下箭头键，您可以导航窗口中。 如果使用这些密钥以离开页面，将显示一个新页面。

反汇编窗口中有一个包含两个按钮以及一个具有其他命令的快捷菜单的工具栏。 若要访问菜单，请右键单击标题栏或单击显示的窗口 （在右上角附近的图标![显示反汇编窗口工具栏上的快捷菜单按钮的屏幕截图](images/tbdisasm2.png))。 以下列表介绍了一些菜单命令：

-   **转到当前地址**打开源窗口，其中对应于反汇编窗口中的所选行并突出显示此行的源文件。

-   **在当前指令之前反汇编**导致要放置中间反汇编窗口的当前行。 此命令是默认选项。 如果清除此命令，则当前行将出现在反汇编窗口，从而可节省时间，因为反向方向反汇编可能非常耗时的顶部。

-   **突出显示当前的源行中的说明**使所有对应于当前的源行，以突出显示的说明。 通常情况下，包含一个源行将对应于多个程序集指令。 如果代码已经过优化，这些程序集指令可能不是连续的。 此命令可查找所有从当前源行组合的说明。

-   **显示每个指令的源行**显示每个程序集指令对应的源行号。

-   **显示每个指令的源文件**显示每个程序集指令对应的源代码文件名称。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关程序集的详细信息的调试和相关的命令和程序集显示的完整说明请参阅[在程序集模式下调试](debugging-in-assembly-mode.md)。

 

 





