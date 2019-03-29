---
title: 在 WinDbg 中查看调用堆栈
description: 在 WinDbg 中，可以通过输入命令或通过使用调用窗口中查看调用堆栈。
ms.assetid: 0e5b5611-d43c-40ba-8340-ea49fe18cc3f
keywords:
- 调试信息窗口，调用窗口
- 调用窗口
- 调用堆栈，调用窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f09d3d4a6db2f0103c909bd4c61619cf6e4bb069
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564536"
---
# <a name="viewing-the-call-stack-in-windbg"></a>在 WinDbg 中查看调用堆栈


调用堆栈是导致程序计数器当前位置的函数调用链。 顶级函数在调用堆栈是当前函数下, 一个函数调用当前函数的函数，等等。 调用堆栈显示基于当前的程序计数器，除非您更改寄存器上下文。 有关如何更改寄存器上下文的详细信息，请参阅[更改上下文](changing-contexts.md)。

在 WinDbg 中，可以通过输入命令或通过使用调用窗口中查看调用堆栈。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


可以通过输入之一查看调用堆栈[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)调试器命令窗口中的命令。

## <a name="span-idcallswindowspanspan-idcallswindowspanspan-idcallswindowspancalls-window"></a><span id="Calls_Window"></span><span id="calls_window"></span><span id="CALLS_WINDOW"></span>调用窗口


作为一种替代方法[ **k** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令时，您可以调用窗口中查看调用堆栈。 若要打开调用窗口中，选择**调用堆栈**从**视图**菜单。

下面的屏幕截图显示了调用窗口的一个示例。

![调用窗口的屏幕截图](images/window-calls.png)

## <span id="ddk_calls_window_dbg"></span><span id="DDK_CALLS_WINDOW_DBG"></span>


调用窗口中的按钮，可以自定义调用堆栈的视图。 若要将移动到相应调用中的位置[源窗口](source-window.md)或[反汇编窗口](disassembly-window.md)，双击调用堆栈的行或选择一个行并按 ENTER。 此操作也会更改[本地上下文](changing-contexts.md#local-context)到所选的堆栈帧。 有关运行到或从该点的详细信息，请参阅[控制目标](controlling-the-target.md)。

在用户模式下，堆栈跟踪基于当前线程的堆栈。 有关当前线程的堆栈的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下，堆栈跟踪基于当前寄存器上下文。 可以设置寄存器上下文以匹配特定线程、 上下文记录或捕获帧。 有关设置寄存器上下文的详细信息，请参阅[注册上下文](changing-contexts.md#register-context)。

调用窗口具有一个包含多个按钮和具有带其他命令的快捷菜单的工具栏。 若要访问此菜单中，右键单击标题栏或单击窗口 （在右上角附近的图标![显示调用窗口工具栏上的快捷菜单按钮的屏幕截图](images/tbcall.png))。 工具栏和菜单包含以下按钮和命令：

-   **原始 args**显示传递给函数的前三个参数。 在基于 x86 的处理器上，此显示内容包括传递给函数 ("Args 为子级") 的前三个参数。

-   **Func 信息**显示帧指针省略 (FPO) 数据和其他有关函数的内部信息。 此命令为仅在基于 x86 的处理器上可用。

-   **源**显示源模块名称和函数名称后的行号 （如果调试器已此信息）。

-   **Addrs**显示各种与帧相关的地址。 在基于 x86 的处理器上，此显示内容包括有关堆栈帧 ("ChildEBP") 和寄信人地址 ("RetAddr") 的基指针。

-   **非易失性 regs**显示寄存器上下文的非易失性部分。 此命令为仅在基于 Itanium 处理器上可用。

-   **帧 nums**显示帧号码。 帧是始终连续编号，从零开始。

-   **参数类型**显示有关预期和接收的堆栈中的函数的参数的详细的信息。

-   **始终浮点**将使窗口停靠，即使仍拖到停靠位置。

-   **移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关寄存器上下文和本地上下文的详细信息，请参阅[更改上下文](changing-contexts.md)。

 

 





