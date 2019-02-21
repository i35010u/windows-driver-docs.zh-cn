---
title: 控制进程服务器会话
description: 控制进程服务器会话
ms.assetid: 4219b08a-d353-43dc-8640-96c504b8075b
keywords:
- 控制会话的进程服务器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c193ba0539d8fed3ce7ff2c934275a4f32009da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547470"
---
# <a name="controlling-a-process-server-session"></a>控制进程服务器会话


## <span id="ddk_controlling_a_process_server_session_dbg"></span><span id="DDK_CONTROLLING_A_PROCESS_SERVER_SESSION_DBG"></span>


启动远程会话后，就像它已调试一台计算机上的目标应用程序可以使用智能客户端。 所有命令的都行为将与它们在此情况下，不过，路径是相对于智能客户端的计算机。

### <a name="span-idusingwindbgasasmartclientspanspan-idusingwindbgasasmartclientspanusing-windbg-as-a-smart-client"></a><span id="using_windbg_as_a_smart_client"></span><span id="USING_WINDBG_AS_A_SMART_CLIENT"></span>充当智能客户端使用 WinDbg

为用户模式进程服务器的智能客户端启动的 WinDbg 后，它将保持附加到进程服务器永久。 如果在调试会话结束，[文件 |附加到进程](file---attach-to-a-process.md)菜单命令或[ **.tlist (列表进程 Id)** ](-tlist--list-process-ids-.md)命令将显示运行进程服务器的计算机上运行的所有进程。 可以将 WinDbg 附加到其中的任何进程。

[文件 |打开可执行文件](file---open-executable.md)命令不能使用。 如果它包含在 WinDbg 命令行上，可以仅生成一个新的进程。

在此情况下，WinDbg 将不能调试其中正在运行，也将能够启动内核调试会话的计算机上的进程。

### <a name="span-idendingthesessionspanspan-idendingthesessionspanending-the-session"></a><span id="ending_the_session"></span><span id="ENDING_THE_SESSION"></span>结束会话

CDB 或 WinDbg 可以退出或结束调试会话以正常方式。 请参阅[结束调试会话在 WinDbg 中](ending-a-debugging-session-in-windbg.md)有关详细信息。 进程服务器将继续正常工作，并可根据需要多次重复使用。 （它还可通过为任意数量的同时调试会话。）

可以从任一计算机终止进程服务器。 若要终止它从智能客户端，使用[ **.endpsrv （结束进程服务器）** ](-endpsrv--end-process-server-.md)命令。 若要终止进程服务器运行的计算机中，使用任务管理器结束 dbgsrv.exe 进程。

 

 





