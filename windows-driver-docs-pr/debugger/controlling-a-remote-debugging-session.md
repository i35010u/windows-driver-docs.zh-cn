---
title: 控制远程调试会话
description: 控制远程调试会话
ms.assetid: dedd277d-1aa0-468c-919c-29b25b0b5c0d
keywords:
- 通过调试器，控制会话的远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 165f4973c870d4071942521f4eb87e27672d7a94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375537"
---
# <a name="controlling-a-remote-debugging-session"></a>控制远程调试会话


## <span id="ddk_controlling_a_remote_debugging_session_dbg"></span><span id="DDK_CONTROLLING_A_REMOTE_DEBUGGING_SESSION_DBG"></span>


启动远程会话后，可以调试服务器或调试客户端中输入命令。 如果有多个客户端，其中任何一个可以输入命令。 按下 ENTER 后，该命令是传输到调试服务器并执行。

每当一个用户输入命令时，所有用户都会都看到命令本身和它的输出。 如果此命令从调试客户端颁发，所有其他用户将查看标识，上述命令的执行的命令的用户。 从调试服务器发出的命令不具有此前缀。

由一个用户执行命令后，通过 KD 或 CDB 连接其他用户将不会看到新的命令提示符。 但是，用户的 WinDbg 时将看到调试器命令窗口的底部面板中的提示符下持续，甚至调试器引擎处于运行状态。 这两个命令应该是一个会发出警报;任何用户可以在任何时候，输入命令，引擎将按接收的顺序执行这些命令。

通过接口还将执行调试服务器 WinDbg 进行的操作。

### <a name="span-idcommunicationbetweenusersspanspan-idcommunicationbetweenusersspancommunication-between-users"></a><span id="communication_between_users"></span><span id="COMMUNICATION_BETWEEN_USERS"></span>用户之间的通信

每当新的调试客户端连接到会话时，所有其他用户将看到一条消息，此客户端已连接。 当客户端断开连接时，不显示任何消息。

[ **.Clients （列表调试客户端）** ](-clients--list-debugging-clients-.md)命令将列出当前已连接到调试会话的所有客户端。

[ **.Echo （Echo 注释）** ](-echo--echo-comment-.md)命令可用于将消息从一个用户发送到另一个。

### <a name="span-idwindbgworkspacesspanspan-idwindbgworkspacesspanwindbg-workspaces"></a><span id="windbg_workspaces"></span><span id="WINDBG_WORKSPACES"></span>WinDbg Workspaces

当 WinDbg 用作调试客户端时，其工作区将仅保存通过图形界面设置的值。 通过调试器命令窗口所做的更改将不保存。 （这可确保，仅通过本地客户端所做的更改都将反映，因为调试器命令窗口将接受来自所有客户端，以及调试服务器的输入。）

### <a name="span-idfilepathsspanspan-idfilepathsspanfile-paths"></a><span id="file_paths"></span><span id="FILE_PATHS"></span>文件路径

符号路径、 可执行映像路径和扩展 DLL 路径被解释为相对于调试服务器上的 Windows 调试工具安装文件夹的文件路径。

当 WinDbg 用作调试客户端时，它具有自己*本地源路径*也。 所有源相关的命令将都访问本地计算机上的源文件。 因此，需要在任何客户端或服务器，将使用源命令上设置的正确路径。

此多个路径系统允许调试客户端使用与源相关的命令而无需实际与其他客户端或服务器共享的源文件。 这是有私有或机密的源文件，其中一个用户有权访问这些文件的情况下很有用。

### <a name="span-idcancelingthedebuggingserverspanspan-idcancelingthedebuggingserverspancanceling-the-debugging-server"></a><span id="canceling_the_debugging_server"></span><span id="CANCELING_THE_DEBUGGING_SERVER"></span>正在取消调试服务器

[ **.Endsrv (结束调试 Server)** ](-endsrv--end-debugging-server-.md)命令可用于终止调试服务器。 如果调试器已建立多个调试服务器，则可以取消了一部分而其他运行。

正在终止服务器将阻止任何将来的客户端将附加到它。 它不会截断了当前连接到服务器的任何客户端。

### <a name="span-idexitingthedebuggerandterminatingthesessionspanspan-idexitingthedebuggerandterminatingthesessionspanexiting-the-debugger-and-terminating-the-session"></a><span id="exiting_the_debugger_and_terminating_the_session"></span><span id="EXITING_THE_DEBUGGER_AND_TERMINATING_THE_SESSION"></span>退出调试器并终止会话

若要从一个调试客户端退出而不终止服务器，必须从该特定客户端发出命令。 如果此客户端 KD 或 CDB，请使用[ **CTRL + B** ](ctrl-b--quit-local-debugger-.md)键退出。 如果使用脚本来运行 KD 或 CDB，使用[ **.remote\_退出 （退出调试客户端）**](-remote-exit--exit-debugging-client-.md)。 如果此客户端 WinDbg，请选择**退出**从**文件**菜单以退出。

若要终止整个会话并退出调试服务器，请使用[ **q (Quit)** ](q--qq--quit-.md)命令。 可以从任何服务器或客户端中，输入此命令，它将终止所有用户的整个会话。

 

 





