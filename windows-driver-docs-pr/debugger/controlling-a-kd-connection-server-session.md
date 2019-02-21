---
title: 控制 KD 连接服务器会话
description: 控制 KD 连接服务器会话
ms.assetid: d927575f-f408-48d0-81f4-0711a09b0015
keywords:
- 控制会话的 KD 连接服务器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66343156fd13ace296c6aed7f7079df155e60b55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520718"
---
# <a name="controlling-a-kd-connection-server-session"></a>控制 KD 连接服务器会话


## <span id="ddk_controlling_a_kd_connection_server_session_dbg"></span><span id="DDK_CONTROLLING_A_KD_CONNECTION_SERVER_SESSION_DBG"></span>


启动远程会话后，智能客户端可以使用像它已调试的计算机的目标计算机在 KD 连接服务器运行。 所有命令的都行为将与它们在此情况下，不过，路径是相对于智能客户端的计算机。

### <a name="span-idusingwindbgasasmartclientspanspan-idusingwindbgasasmartclientspanusing-windbg-as-a-smart-client"></a><span id="using_windbg_as_a_smart_client"></span><span id="USING_WINDBG_AS_A_SMART_CLIENT"></span>充当智能客户端使用 WinDbg

WinDbg KD 连接服务器的智能客户端启动后，可以使用[调试 |停止调试](debug---stop-debugging.md)命令以结束调试会话。 此时，WinDbg 将进入休眠模式，并且将无法再连接到 KD 连接服务器。 将 WinDbg 正在其中运行的计算机上完成所有的后续调试。 您不能重新附加到 KD 连接提供通过使用[文件 |内核调试](file---kernel-debug.md)-此设置只能从命令行。

### <a name="span-idendingthesessionspanspan-idendingthesessionspanending-the-session"></a><span id="ending_the_session"></span><span id="ENDING_THE_SESSION"></span>结束会话

KD 或 WinDbg 可以退出或结束调试会话以正常方式。 请参阅[结束调试会话在 WinDbg 中](ending-a-debugging-session-in-windbg.md)

有关详细信息。 KD 连接服务器将继续正常工作，并可根据需要多次重复使用。 （它还可通过为任意数量的同时调试会话。）

可以从任一计算机终止 KD 连接服务器。 若要终止它从智能客户端，使用[ **.endpsrv （结束进程服务器）** ](-endpsrv--end-process-server-.md)命令。 若要终止 KD 连接服务器运行的计算机中，使用任务管理器结束 kdsrv.exe 进程。

 

 





