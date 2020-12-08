---
title: 控制远程调试会话
description: 控制远程调试会话
keywords:
- 通过调试器远程调试，控制会话
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d16cb0e3ad76b6df9cebdfe07382b56f211cb824
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819199"
---
# <a name="controlling-a-remote-debugging-session"></a>控制远程调试会话


## <span id="ddk_controlling_a_remote_debugging_session_dbg"></span><span id="DDK_CONTROLLING_A_REMOTE_DEBUGGING_SESSION_DBG"></span>


远程会话启动后，可以将命令输入调试服务器或调试客户端。 如果有多个客户端，则可以输入命令。 按下 ENTER 后，该命令将传输到调试服务器并执行。

每当用户输入一个命令时，所有用户都将看到该命令本身和输出。 如果此命令是从调试客户端发出的，则所有其他用户都将在发出该命令的用户的命令前面看到标识。 从调试服务器发出的命令没有此前缀。

一个用户执行命令后，通过 KD 或 CDB 连接的其他用户将看不到新的命令提示符。 另一方面，即使调试器引擎正在运行，也会在调试器的底部面板中看到该提示命令窗口连续运行。 这二者都不是警报的原因;任何用户都可以随时输入命令，引擎将按接收顺序执行这些命令。

通过 WinDbg 接口执行的操作还将由调试服务器执行。

### <a name="span-idcommunication_between_usersspanspan-idcommunication_between_usersspancommunication-between-users"></a><span id="communication_between_users"></span><span id="COMMUNICATION_BETWEEN_USERS"></span>用户之间的通信

每当新的调试客户端连接到该会话时，所有其他用户都会看到一条消息，指出该客户端已连接。 当客户端断开连接时，不会显示任何消息。

[**. Clients (List 调试客户端)**](-clients--list-debugging-clients-.md)命令将列出当前连接到调试会话的所有客户端。

[**回显 (Echo Comment)**](-echo--echo-comment-.md)命令可用于将消息从一个用户发送到另一个用户。

### <a name="span-idwindbg_workspacesspanspan-idwindbg_workspacesspanwindbg-workspaces"></a><span id="windbg_workspaces"></span><span id="WINDBG_WORKSPACES"></span>WinDbg 工作区

当 WinDbg 用作调试客户端时，它的工作区只保存通过图形界面设置的值。 不会保存通过调试器命令窗口所做的更改。  (这可以保证只会反映本地客户端所做的更改，因为调试器命令窗口会接受来自所有客户端以及调试服务器的输入。 ) 

### <a name="span-idfile_pathsspanspan-idfile_pathsspanfile-paths"></a><span id="file_paths"></span><span id="FILE_PATHS"></span>文件路径

符号路径、可执行图像路径和扩展 DLL 路径都解释为相对于调试服务器上的 Windows 安装的调试工具文件夹的文件路径。

当 WinDbg 用作调试客户端时，它还具有自己的 *本地源路径* 。 所有与源相关的命令都将访问本地计算机上的源文件。 因此，必须在将使用源命令的任何客户端或服务器上设置正确的路径。

此多路径系统允许调试客户端使用源相关的命令，而不会与其他客户端或服务器进行实际共享。 如果有一个用户有权访问的私有或机密源文件，这会很有用。

### <a name="span-idcanceling_the_debugging_serverspanspan-idcanceling_the_debugging_serverspancanceling-the-debugging-server"></a><span id="canceling_the_debugging_server"></span><span id="CANCELING_THE_DEBUGGING_SERVER"></span>取消调试服务器

[**Endsrv (End 调试服务器)**](-endsrv--end-debugging-server-.md)命令可用于终止调试服务器。 如果调试器已建立多个调试服务器，您可以取消其中一些调试服务器，而让其他调试服务器保持运行状态。

终止服务器将阻止任何将来的客户端连接到该服务器。 它不会切断当前通过服务器连接的所有客户端。

### <a name="span-idexiting_the_debugger_and_terminating_the_sessionspanspan-idexiting_the_debugger_and_terminating_the_sessionspanexiting-the-debugger-and-terminating-the-session"></a><span id="exiting_the_debugger_and_terminating_the_session"></span><span id="EXITING_THE_DEBUGGER_AND_TERMINATING_THE_SESSION"></span>退出调试器并终止会话

若要在不终止服务器的情况下退出一个调试客户端，则必须从该特定客户端发出一个命令。 如果此客户端为 KD 或 CDB，请使用 [**CTRL + B**](ctrl-b--quit-local-debugger-.md) 键退出。 如果使用脚本运行 KD 或 CDB，请使用 [**remote \_ Exit (退出调试客户端)**](-remote-exit--exit-debugging-client-.md)。 如果此客户端为 WinDbg，请从 "**文件**" 菜单中选择 "**退出**" 以退出。

若要终止整个会话并退出调试服务器，请使用 [**q (Quit)**](q--qq--quit-.md) 命令。 此命令可从任何服务器或客户端输入，并将终止所有用户的整个会话。

 

 





