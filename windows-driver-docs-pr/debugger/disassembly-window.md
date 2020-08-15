---
title: 在 WinDbg 中进行程序集代码调试
description: 在 WinDbg 中，可以通过输入命令或使用 "反汇编" 窗口来查看程序集代码。
ms.assetid: e00ea29e-4153-4588-8353-de69910bfc65
keywords:
- 调试信息窗口，"反汇编" 窗口
- “反汇编”窗口
- 程序集调试，反汇编窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78441a68380019f9e499013ecf883ba6753b3cd9
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252985"
---
# <a name="assembly-code-debugging-in-windbg"></a>在 WinDbg 中进行程序集代码调试


在 WinDbg 中，可以通过输入命令或使用 "反汇编" 窗口来查看程序集代码。

## <a name="span-iddebugger_command_windowspanspan-iddebugger_command_windowspanspan-iddebugger_command_windowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


可以通过在调试器命令窗口中输入 [**u、ub、uu (Unassemble) **](u--unassemble-.md) 命令之一来查看程序集代码。

## <a name="span-idddk_disassembly_window_dbgspanspan-idddk_disassembly_window_dbgspandissasembly-window"></a><span id="ddk_disassembly_window_dbg"></span><span id="DDK_DISASSEMBLY_WINDOW_DBG"></span>Dissasembly 窗口


若要打开或切换到 "反汇编" 窗口，请从 "**视图**" 菜单中选择 " **Dissasembly** "。  (还可以按 ALT + 7，或在**Disassembly** ![ ](images/tbdisasm2.png) 工具栏上的 "反汇编" 按钮)  (屏幕截图中选择 "反汇编" 按钮。 ALT + SHIFT + 7 将关闭 "反汇编" 窗口。 ) 

下面的屏幕截图显示了一个 "反汇编" 窗口示例。

!["反汇编" 窗口的屏幕截图](images/window-disassembly.png)

调试器将获取一个内存部分，将它解释为二进制计算机指令，然后将其反汇编，以生成计算机指令的汇编语言版本。 生成的代码将显示在 "反汇编" 窗口中。

在 "反汇编" 窗口中，您可以执行以下操作：

-   若要反汇编不同的内存部分，请在 " **偏移量** " 框中键入要反汇编的内存的地址。  (键入地址后，可以按 ENTER，但不必这样做。 ) "反汇编" 窗口在完成地址之前显示代码;您可以忽略此代码。

-   若要查看内存的其他部分，请选择 " **上一** 步" 或 " **下一步** " 按钮，或者按 PAGE UP 或 page DOWN 键。 这些命令分别显示前面或后面的内存部分中的反汇编代码。 通过按向右箭头、向左键、向上键和向下键，可以在窗口中导航。 如果使用这些键从页面移出，将显示一个新页面。

"反汇编" 窗口包含一个工具栏，其中包含两个按钮和一个包含其他命令的快捷菜单。 若要访问菜单，请选择并按住 (或右键单击标题栏) 或选择出现在窗口右上角附近的图标 (![显示 "反汇编" 窗口工具栏快捷菜单的按钮屏幕截图](images/tbdisasm2.png)). 以下列表描述了一些菜单命令：

-   "**前往当前地址**" 打开源窗口，其中包含与 "反汇编" 窗口中所选行对应的源文件，并突出显示此行。

-   在**当前指令之前进行拆装**会导致当前行位于 "反汇编" 窗口的中间。 此命令是默认选项。 如果清除此命令，则当前行将出现在 "反汇编" 窗口的顶部，这可节省时间，因为反向反汇编可能非常耗时。

-   **突出显示当前源行中的说明** 将导致突出显示与当前源代码行对应的所有说明。 通常，单个源行将对应于多个程序集指令。 如果代码已经过优化，则这些程序集指令可能不是连续的。 此命令可用于查找从当前源行中收集的所有说明。

-   **显示每个指令的源行** 显示对应于每个程序集指令的源行号。

-   **显示每个指令的源文件** 显示对应于每个程序集指令的源文件名。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关程序集调试和相关命令的详细信息以及程序集显示的完整说明，请参阅 [程序集模式下的调试](debugging-in-assembly-mode.md)。

 

 





