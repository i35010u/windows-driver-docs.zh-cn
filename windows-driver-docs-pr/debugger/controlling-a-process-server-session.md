---
title: 控制进程服务器会话
description: 控制进程服务器会话
keywords:
- 进程服务器，控制会话
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 502bfd397c4a6c612d408d3d0f6dc7578310cc92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819219"
---
# <a name="controlling-a-process-server-session"></a>控制进程服务器会话


## <span id="ddk_controlling_a_process_server_session_dbg"></span><span id="DDK_CONTROLLING_A_PROCESS_SERVER_SESSION_DBG"></span>


远程会话启动后，可以像在单个计算机上调试目标应用程序一样使用智能客户端。 除路径相对于智能客户端的计算机而言，所有命令的行为都与在这种情况下的行为相同。

### <a name="span-idusing_windbg_as_a_smart_clientspanspan-idusing_windbg_as_a_smart_clientspanusing-windbg-as-a-smart-client"></a><span id="using_windbg_as_a_smart_client"></span><span id="USING_WINDBG_AS_A_SMART_CLIENT"></span>使用 WinDbg 作为智能客户端

在将 WinDbg 作为用户模式进程服务器的智能客户端启动后，它将永久连接到进程服务器。 如果调试会话结束，则 [文件 |附加到进程](file---attach-to-a-process.md) 菜单命令或 [**Tlist.exe (列出进程 id)**](-tlist--list-process-ids-.md) 命令将显示运行进程服务器的计算机上运行的所有进程。 WinDbg 可以附加到其中任何一个进程。

[文件 |无法使用打开可执行文件](file---open-executable.md)命令。 只有在 WinDbg 命令行中包括新进程时，才能生成该进程。

在这种情况下，WinDbg 将无法在运行该进程的计算机上调试进程，也无法启动内核调试会话。

### <a name="span-idending_the_sessionspanspan-idending_the_sessionspanending-the-session"></a><span id="ending_the_session"></span><span id="ENDING_THE_SESSION"></span>结束会话

CDB 或 WinDbg 可以正常退出或结束调试会话。 有关详细信息，请参阅 [在 WinDbg 结束调试会话](ending-a-debugging-session-in-windbg.md) 。 进程服务器将继续运行，并可根据需要多次重复使用。  (还可将其用于任意数量的同时调试会话。 ) 

进程服务器可以从任一计算机上终止。 若要从智能客户端中终止它，请使用 [**endpsrv (结束进程服务器)**](-endpsrv--end-process-server-.md) 命令。 若要从运行它的计算机中终止进程服务器，请使用 "任务管理器" 来结束 dbgsrv.exe 进程。

 

 





