---
title: 控制 KD 连接服务器会话
description: 控制 KD 连接服务器会话
keywords:
- KD 连接服务器，控制会话
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215701b766526febb61492b0ad5ea90b1aad69f2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819221"
---
# <a name="controlling-a-kd-connection-server-session"></a>控制 KD 连接服务器会话


## <span id="ddk_controlling_a_kd_connection_server_session_dbg"></span><span id="DDK_CONTROLLING_A_KD_CONNECTION_SERVER_SESSION_DBG"></span>


启动远程会话后，可以使用智能客户端，就像从运行 KD 连接服务器的计算机调试目标计算机一样。 除路径相对于智能客户端的计算机而言，所有命令的行为都与在这种情况下的行为相同。

### <a name="span-idusing_windbg_as_a_smart_clientspanspan-idusing_windbg_as_a_smart_clientspanusing-windbg-as-a-smart-client"></a><span id="using_windbg_as_a_smart_client"></span><span id="USING_WINDBG_AS_A_SMART_CLIENT"></span>使用 WinDbg 作为智能客户端

将 WinDbg 作为 KD 连接服务器的智能客户端启动后，可以使用 "调试" [|停止调试](debug---stop-debugging.md) 命令以结束调试会话。 此时，WinDbg 将进入休眠模式，并且将不再连接到 KD 连接服务器。 所有后续调试都将在运行 WinDbg 的计算机上完成。 不能使用文件重新附加到 KD 连接服务 [|内核调试](file---kernel-debug.md) -仅可以从命令行执行此操作。

### <a name="span-idending_the_sessionspanspan-idending_the_sessionspanending-the-session"></a><span id="ending_the_session"></span><span id="ENDING_THE_SESSION"></span>结束会话

KD 或 WinDbg 可以正常退出或结束调试会话。 请参阅 [在 WinDbg 结束调试会话](ending-a-debugging-session-in-windbg.md)

以获取详细信息。 KD 连接服务器将继续运行，并可根据需要多次重复使用。  (还可将其用于任意数量的同时调试会话。 ) 

可以从任意一台计算机中终止 KD 连接服务器。 若要从智能客户端中终止它，请使用 [**endpsrv (结束进程服务器)**](-endpsrv--end-process-server-.md) 命令。 若要从运行它的计算机中终止 KD 连接服务器，请使用任务管理器结束 kdsrv.exe 进程。

 

 





