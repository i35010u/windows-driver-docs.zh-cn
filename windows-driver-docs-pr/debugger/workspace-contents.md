---
title: 工作区内容
description: 工作区内容
ms.assetid: aa0a3bab-2907-4bcf-9a48-5669c423447a
keywords:
- 工作区，工作区的内容
- 自动启动会话的工作区
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 591693a2b54a1eeecb3dd66cc39748976c058d2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562189"
---
# <a name="workspace-contents"></a>工作区内容


## <span id="ddk_workspace_contents_dbg"></span><span id="DDK_WORKSPACE_CONTENTS_DBG"></span>


每个工作区保留有关当前调试会话的以下信息。 从基本的工作区开始和结束的最近加载的工作区，将累积，应用此信息。

-   有关异常和事件的所有中断和处理信息。 有关详细信息的中断和处理信息，请参阅工作区中的断点。

-   所有开放源代码文件。 如果找不到源文件，将显示一条错误消息。 您可以关闭这些错误消息，单独或通过使用[窗口 |关闭所有错误 Windows](window---close-all-error-windows.md)命令。

-   用户定义的所有别名。

每个工作区保留有关调试器的配置设置的以下信息。 从基本的工作区开始和结束的最近加载的工作区，将累积，应用此信息。

-   符号路径中。

-   可执行映像路径中。

-   源路径中。 （在远程调试的主要源路径和本地源路径会保存。）

-   设置了当前源选项[ **l +，l-（设置源选项）**](l---l---set-source-options-.md)。

-   日志文件设置。

-   COM 或 1394年内核连接设置，如果通过使用图形界面开始连接。

-   在每个最新的路径**打开**（除外的工作区中文件和文本文件路径，不保存） 对话框。

-   当前[ **.enable\_unicode**](-enable-unicode--enable-unicode-display-.md)， [ **.force\_基数\_输出**](-force-radix-output--use-radix-for-integers-.md)，和[**.enable\_长\_状态**](-enable-long-status--enable-long-integer-display-.md)设置。

所有默认工作区和命名工作区都保留有关 WinDbg 图形界面的以下信息。 从基本的工作区开始和结束的最近加载的工作区会累积，加载此信息。

-   WinDbg 窗口的标题

-   [会自动打开反汇编](window---automatically-open-disassembly.md)设置

-   默认字体

所有默认工作区和命名工作区都保留有关 WinDbg 图形界面的以下信息。 此信息不累积应用。 它取决于仅在最近加载的工作区。

-   大小和 WinDbg 窗口在桌面上的位置。

-   调试信息窗口处于打开状态。

-   大小和每个位置打开窗口，其中包括窗口的大小，其浮动或停靠状态，是否使用其他窗口中，在其快捷菜单中的相关设置的所有选项卡式。

-   中的窗格边界的位置[调试器命令窗口](debugger-command-window.md)和包装在该窗口中设置一词。

-   工具栏和状态栏以及每个调试的信息窗口上的单个工具栏是否可见。

-   自定义[寄存器窗口](registers-window.md)。

-   中的标志[调用窗口](calls-window.md)，局部变量窗口和监视窗口。

-   在监视窗口中查看项。

-   在每个光标所在的位置[源窗口](source-window.md)。

### <a name="span-idnamedworkspacesspanspan-idnamedworkspacesspannamed-workspaces"></a><span id="named_workspaces"></span><span id="NAMED_WORKSPACES"></span>命名工作区

命名工作区包含未存储在默认工作区的其他信息。

此附加信息包括有关当前会话状态信息。 保存指定的工作区后，将保存当前会话。 如果更高版本打开此工作区，则此会话将自动重启。

您可以开始仅内核调试，调试和生成的用户模式进程以这种方式调试转储文件。 远程会话和用户模式进程，调试器附加到不具有在其工作区中保存此会话信息。

如果另一个会话已处于活动状态，无法打开这种类型的指定的工作区。

### <a name="span-iddebuggingclientsandworkspacesspanspan-iddebuggingclientsandworkspacesspandebugging-clients-and-workspaces"></a><span id="debugging_clients_and_workspaces"></span><span id="DEBUGGING_CLIENTS_AND_WORKSPACES"></span>调试客户端和工作区

当作为调试客户端使用 WinDbg 时，其工作区将保存通过图形界面设置的值。 不保存所做的更改通过调试器命令窗口。 （此限制保证仅本地客户端所做的更改已反映，因为调试器命令窗口接受输入的所有客户端和调试服务器。）有关详细信息，请参阅[控制远程调试会话](controlling-a-remote-debugging-session.md)。

### <a name="span-idbreakpointsinworkspacesspanspan-idbreakpointsinworkspacesspanbreakpoints-in-workspaces"></a><span id="breakpoints_in_workspaces"></span><span id="BREAKPOINTS_IN_WORKSPACES"></span>工作区中的断点

此外，断点信息保存在工作区，包括中断地址和状态。 下一个会话启动时，在会话结束时处于活动状态的断点处于活动状态。 但是，某些遇到这些断点可能无法解析如果尚未加载正确的模块。

符号表达式，按行号、 通过数字地址，或通过使用鼠标在源窗口中指定的断点均保存在工作区中。 通过使用鼠标在反汇编或调用窗口中指定的断点不会保存在工作区。

如果你正在调试多个用户模式进程，将保存与零进程关联的断点。

 

 





