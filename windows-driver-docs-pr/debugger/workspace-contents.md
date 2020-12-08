---
title: 工作区内容
description: 工作区内容
keywords:
- 工作区，工作区的内容
- 工作区，自动启动会话
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec0528112c48d089ec17df35c480deb31071484
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802777"
---
# <a name="workspace-contents"></a>工作区内容


## <span id="ddk_workspace_contents_dbg"></span><span id="DDK_WORKSPACE_CONTENTS_DBG"></span>


每个工作区都保留有关当前调试会话的下列信息。 此信息累积应用，从基本工作区开始，到最近加载的工作区结束。

-   异常和事件的所有中断和处理信息。 有关中断和处理信息的详细信息，请参阅工作区中的断点。

-   所有打开的源文件。 如果找不到源文件，将显示一条错误消息。 您可以单独或使用窗口关闭这些错误消息 [|关闭所有错误 Windows](window---close-all-error-windows.md) 命令。

-   所有用户定义的别名。

每个工作区都保留有关调试器配置设置的下列信息。 此信息累积应用，从基本工作区开始，到最近加载的工作区结束。

-   符号路径。

-   可执行映像路径。

-   源路径。  (在远程调试中，将保存主源路径和本地源路径。 ) 

-   用 [**l +、l (集源选项**](l---l---set-source-options-.md)设置的当前源选项) 。

-   日志文件设置。

-   COM 或1394内核连接设置（如果连接是使用图形界面启动的）。

-   每个 **打开** 的对话框中的最新路径 (除了工作区文件和文本文件路径以外，不会) 保存。

-   当前的 [**. 启用 \_ unicode**](-enable-unicode--enable-unicode-display-.md)、 [**强制执行 \_ 基数 \_ 输出**](-force-radix-output--use-radix-for-integers-.md)和 [**。启用 \_ 长 \_ 状态**](-enable-long-status--enable-long-integer-display-.md) 设置。

所有默认工作区和命名工作区保留有关 WinDbg 图形界面的以下信息。 此信息是累积加载的，从基本工作区开始，到最后加载的工作区结束。

-   WinDbg 窗口的标题

-   [自动打开的反汇编](window---automatically-open-disassembly.md)设置

-   默认字体

所有默认工作区和命名工作区保留有关 WinDbg 图形界面的以下信息。 此信息不会累积应用。 它仅依赖于最近加载的工作区。

-   WinDbg 窗口在桌面上的大小和位置。

-   打开了哪些调试信息窗口。

-   每个打开窗口的大小和位置，包括窗口的大小、其浮动或停靠状态、是否与其他窗口一起选项卡以及其快捷菜单中的所有相关设置。

-   窗格边界在调试器中的位置 [命令窗口](debugger-command-window.md) 和该窗口中的自动换行设置。

-   工具栏和状态栏以及每个 "调试信息" 窗口上的各个工具栏是否可见。

-   " [寄存器" 窗口](registers-window.md)的自定义。

-   " [调用" 窗口](calls-window.md)、"局部变量" 窗口和监视窗口中的标志。

-   在监视窗口中查看的项。

-   每个 [源窗口](source-window.md)中的光标位置。

### <a name="span-idnamed_workspacesspanspan-idnamed_workspacesspannamed-workspaces"></a><span id="named_workspaces"></span><span id="NAMED_WORKSPACES"></span>命名工作区

命名工作区包含未存储在默认工作区中的其他信息。

此附加信息包括有关当前会话状态的信息。 保存命名工作区后，将保存当前会话。 如果稍后打开此工作区，此会话将自动重启。

您只能以这种方式启动内核调试、转储文件调试和生成的用户模式进程。 调试器附加到的远程会话和用户模式进程不会将此会话信息保存在其工作区中。

如果其他会话已经处于活动状态，则无法打开这种命名的工作区。

### <a name="span-iddebugging_clients_and_workspacesspanspan-iddebugging_clients_and_workspacesspandebugging-clients-and-workspaces"></a><span id="debugging_clients_and_workspaces"></span><span id="DEBUGGING_CLIENTS_AND_WORKSPACES"></span>调试客户端和工作区

使用 WinDbg 作为调试客户端时，其工作区仅保存通过图形界面设置的值。 不会保存通过调试器命令窗口所做的更改。  (此限制保证仅反映本地客户端所做的更改，因为调试器命令窗口接受来自所有客户端和调试服务器的输入。 ) 有关详细信息，请参阅 [控制远程调试会话](controlling-a-remote-debugging-session.md)。

### <a name="span-idbreakpoints_in_workspacesspanspan-idbreakpoints_in_workspacesspanbreakpoints-in-workspaces"></a><span id="breakpoints_in_workspaces"></span><span id="BREAKPOINTS_IN_WORKSPACES"></span>工作区中的断点

此外，断点信息保存在工作区中，包括中断地址和状态。 会话结束时处于活动状态的断点在下一个会话启动时处于活动状态。 但是，如果尚未加载适当的模块，其中某些断点可能无法解析。

由符号表达式、行号、数字地址指定的断点，或者在源窗口中使用鼠标的断点都保存在工作区中。 在 "反汇编" 窗口或 "调用" 窗口中使用鼠标指定的断点不会保存在工作区中。

如果正在调试多个用户模式进程，则只保存与进程0关联的断点。

 

 





