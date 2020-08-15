---
title: 在 WinDbg 中查看调用堆栈
description: 在 WinDbg 中，可以通过输入命令或使用 "调用" 窗口来查看调用堆栈。
ms.assetid: 0e5b5611-d43c-40ba-8340-ea49fe18cc3f
keywords:
- 调试信息窗口，调用窗口
- 调用窗口
- 调用堆栈，调用窗口
ms.date: 05/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 642ac02f1287e13c9f468c6693f40f7b223c7045
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252845"
---
# <a name="viewing-the-call-stack-in-windbg"></a>在 WinDbg 中查看调用堆栈


调用堆栈是已导致程序计数器当前位置的函数调用的链。 调用堆栈上的 top 函数是当前函数，下一个函数是调用当前函数的函数，依此类推。 显示的调用堆栈基于当前程序计数器，除非更改寄存器上下文。 有关如何更改注册上下文的详细信息，请参阅 [更改上下文](changing-contexts.md)。

在 WinDbg 中，可以通过输入命令或使用 "调用" 窗口来查看调用堆栈。

## <a name="span-iddebugger_command_windowspanspan-iddebugger_command_windowspanspan-iddebugger_command_windowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口


您可以通过在调试器命令窗口中输入其中一个 [**k (显示堆栈 Backtrace) **](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来查看调用堆栈。

## <a name="span-idcalls_windowspanspan-idcalls_windowspanspan-idcalls_windowspancalls-window"></a><span id="Calls_Window"></span><span id="calls_window"></span><span id="CALLS_WINDOW"></span>调用窗口


作为 [**k**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令的替代方法，可以在调用窗口中查看调用堆栈。 若要打开 "调用" 窗口，请从 "**视图**" 菜单中选择 "**调用堆栈**"。

以下屏幕截图显示了 "调用" 窗口的示例。

!["调用" 窗口的屏幕截图](images/window-calls.png)

## <span id="ddk_calls_window_dbg"></span><span id="DDK_CALLS_WINDOW_DBG"></span>


使用 "调用" 窗口中的按钮可以自定义调用堆栈的视图。 若要移动到 [源窗口](source-window.md) 或 " [反汇编" 窗口](disassembly-window.md)中的相应调用位置，请双击调用堆栈的行，或者选择一行，然后按 enter。 此操作还会将 [本地上下文](changing-contexts.md#local-context) 更改为所选的堆栈帧。 有关运行到或从此点运行的详细信息，请参阅 [控制目标](controlling-the-target.md)。

在用户模式下，堆栈跟踪基于当前线程的堆栈。 有关当前线程的堆栈的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下，堆栈跟踪基于当前的注册表上下文。 您可以将注册上下文设置为与特定线程、上下文记录或捕获帧匹配。 有关设置寄存器上下文的详细信息，请参阅 [注册上下文](changing-contexts.md#register-context)。

"调用" 窗口包含一个工具栏，其中包含多个按钮，并具有包含附加命令的快捷菜单。 若要访问此菜单，请选择并按住 (或右键单击标题栏) 或选择窗口右上角附近的图标 (![显示 "调用" 窗口工具栏快捷菜单的按钮屏幕截图](images/tbcall.png)). 工具栏和菜单包含以下按钮和命令：

-   **原始参数** 显示传递到函数的前三个参数。 在基于 x86 的处理器上，此显示内容包括传递给函数 ( "Args to Child" ) 的前三个参数。

-   **Func info** 显示了帧指针省略 (FPO) 数据以及有关函数的其他内部信息。 此命令仅适用于基于 x86 的处理器。

-   **源** 在函数名称后显示源模块名称和行号 (如果调试器将此信息) 。

-   **Addrs** 显示各种帧相关的地址。 在基于 x86 的处理器上，此显示内容包括堆栈帧的基指针 ( "ChildEBP" ) 和返回地址 ( "RetAddr" ) 。

-   **帧 nums** 显示帧号。 帧始终连续编号，从零开始。

-   **Arg 类型** 显示有关堆栈中的函数应和收到的参数的详细信息。

-   **始终浮动** 会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   "**移动到帧**" 会导致在移动 WinDbg 帧时窗口移动，即使窗口未停靠也是如此。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关寄存器上下文和本地上下文的详细信息，请参阅 [更改上下文](changing-contexts.md)。

 

 





