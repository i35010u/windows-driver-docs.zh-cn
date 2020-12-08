---
title: 远程目标
description: 远程目标
keywords:
- 调试器引擎 API、目标、远程
- 调试器引擎 API，调试服务器
- 调试器引擎 API，进程服务器
- 调试器引擎 API，内核连接服务器
- 调试器引擎 API，智能客户端
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39c73b822133879d2d4601ea620450a1833bdfa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791971"
---
# <a name="remote-targets"></a>远程目标


## <span id="ddk_remote_debugging_dbx"></span><span id="DDK_REMOTE_DEBUGGING_DBX"></span>


远程调试有两种不同的形式，具体取决于哪个计算机 (远程客户端或服务器) 是主计算机。 *主计算机* 是 [调试器引擎](introduction.md#debugger-engine)处于活动状态的计算机。 在另一台计算机上，调试器引擎仅充当主机引擎的代理中继命令和数据。

所有调试器操作（如执行命令和 [扩展](introduction.md#extensions)）和符号加载-由主机引擎执行。 调试器会话也相对于主机引擎。

若要列出计算机上当前正在运行的调试服务器和进程服务器，请使用 [**OutputServers**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-outputservers)。

### <a name="span-iddebugging_server_and_debugging_clientspanspan-iddebugging_server_and_debugging_clientspandebugging-servers-and-debugging-clients"></a><span id="debugging_server_and_debugging_client"></span><span id="DEBUGGING_SERVER_AND_DEBUGGING_CLIENT"></span>调试服务器和调试客户端

*调试服务器* 是作为主机并侦听来自调试客户端的连接的调试器引擎实例。 方法 [**StartServer**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-startserver) 将告知调试器引擎开始侦听来自调试客户端的连接。

*调试客户端* 是充当代理的调试器引擎实例，用于向调试服务器发送调试器命令和 i/o。 函数 [**DebugConnect**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect) 可用于连接到调试服务器。

**DebugConnect** 返回的客户端对象不会自动联接到调试服务器上的调试器会话。 方法 [**ConnectSession**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-connectsession) 可用于联接会话、同步输入和输出。

调试服务器和调试客户端之间的通信主要包含发送到服务器的调试器命令和 RPC 调用，以及发送回客户端的命令输出。

### <a name="span-idprocess_server_and_smart_clientspanspan-idprocess_server_and_smart_clientspanprocess-servers-kernel-connection-servers-and-smart-clients"></a><span id="process_server_and_smart_client"></span><span id="PROCESS_SERVER_AND_SMART_CLIENT"></span>进程服务器、内核连接服务器和智能客户端

*进程服务器* 和 *内核连接服务器* 都是充当代理的调试器引擎实例，侦听来自智能客户端的连接，并执行这些远程客户端请求的内存、处理器或操作系统操作。 *进程服务器* 有利于调试在同一台计算机上运行的进程。 *内核连接服务器* 有利于调试连接到运行连接服务器的计算机的 Windows 内核调试目标。 可以使用方法 [**StartProcessServer**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-startprocessserver) 或程序 [DbgSrv](process-servers--user-mode-.md)启动进程服务器。 方法 [**WaitForProcessServerEnd**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-waitforprocessserverend) 将等待 **StartProcessServer** 结束的进程服务器。 可以使用程序 [**KdSrv**](activating-a-kd-connection-server.md)激活内核连接服务器。

*智能客户端* 是充当主机引擎并连接到进程服务器的调试器引擎的实例。 方法 [**ConnectProcessServer**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-connectprocessserver) 将连接到进程服务器。 连接后，可以使用 [Live User-Mode 目标](live-user-mode-targets.md) 中所述的方法。

当远程客户端完成进程服务器时，它可以使用 [**DisconnectProcessServer**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-disconnectprocessserver)断开连接，也可以使用 [**EndProcessServer**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-endprocessserver) 请求进程服务器关闭。 若要从运行进程服务器的计算机上关闭进程服务器，请使用任务管理器来结束进程。 如果使用 **StartProcessServer** 的调试器引擎实例仍在运行，它可以使用 [**Execute**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-execute) 发出调试程序命令 [**。 endsrv 0**](-endsrv--end-debugging-server-.md)，它将结束进程服务器 (这是 **endsrv** 的常见行为，这通常不会影响) 的进程服务器。

进程服务器和智能客户端之间的通信通常由低级内存、处理器以及从远程客户端发送到服务器的操作系统操作和请求组成。 然后，将其结果发送回客户端。

 

