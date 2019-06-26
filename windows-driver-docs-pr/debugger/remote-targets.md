---
title: 远程目标
description: 远程目标
ms.assetid: ed7ea3dc-07d1-481c-90e0-7f0b0e77ad42
keywords:
- 调试器引擎 API、 目标、 远程
- 调试器引擎 API，调试服务器
- 调试器引擎 API，进程服务器
- 调试器引擎 API，内核连接服务器
- 调试器引擎 API，智能客户端
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 327b6cce952b4e8c5eb1a94ef21a89bfb5061fc3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366415"
---
# <a name="remote-targets"></a>远程目标


## <span id="ddk_remote_debugging_dbx"></span><span id="DDK_REMOTE_DEBUGGING_DBX"></span>


有两种不同形式的远程调试，具体取决于哪一台计算机 （远程客户端或服务器） 是主计算机。 *主机计算机*是在其上的计算机[调试器引擎](introduction.md#debugger-engine)处于活动状态。 在其他计算机上，调试器引擎只充当中继命令和主机引擎对数据的代理。

所有调试器操作，例如，执行命令和[扩展](introduction.md#extensions)，和符号加载--由主机引擎执行。 调试器会话也是相对于主机引擎。

若要列出的调试服务器和进程服务器的计算机上当前正在运行，请使用[ **OutputServers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-outputservers)。

### <a name="span-iddebuggingserveranddebuggingclientspanspan-iddebuggingserveranddebuggingclientspandebugging-servers-and-debugging-clients"></a><span id="debugging_server_and_debugging_client"></span><span id="DEBUGGING_SERVER_AND_DEBUGGING_CLIENT"></span>调试服务器和调试客户端

一个*调试服务器*是充当主机和侦听从调试客户端连接的调试器引擎的实例。 该方法[**入门服务器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-startserver)会告知调试器引擎开始侦听来自调试客户端的连接。

一个*调试客户端*是充当代理，将调试器命令和 I/O 发送到调试服务器调试器引擎的实例。 该函数[ **DebugConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugconnect)可用于连接到调试服务器。

返回的客户端对象**DebugConnect**未自动加入到调试服务器上的调试程序会话。 该方法[ **ConnectSession** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-connectsession)可用于加入会话，同步输入和输出。

调试服务器和调试客户端之间的通信主要包括调试器命令和发送到服务器，并发送回客户端的命令输出的 RPC 调用。

### <a name="span-idprocessserverandsmartclientspanspan-idprocessserverandsmartclientspanprocess-servers-kernel-connection-servers-and-smart-clients"></a><span id="process_server_and_smart_client"></span><span id="PROCESS_SERVER_AND_SMART_CLIENT"></span>处理服务器、 内核连接服务器和智能客户端

*进程服务器*并*内核连接服务器*是充当代理，侦听来自智能客户端连接和执行内存、 处理器或操作系统调试器引擎的这两个实例根据这些远程客户端的请求的操作。 一个*进程服务器*帮助调试在同一台计算机运行的进程。 一个*内核连接服务器*帮助调试连接到正在运行连接服务器的计算机的目标是 Windows 内核调试。 可以使用该方法来启动进程服务器[ **StartProcessServer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-startprocessserver)或程序[DbgSrv](process-servers--user-mode-.md)。 该方法[ **WaitForProcessServerEnd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-waitforprocessserverend)将等待的进程服务器入门**StartProcessServer**结束。 可使用该程序激活内核连接服务器[ **KdSrv**](activating-a-kd-connection-server.md)。

一个*智能客户端*已作为主机引擎调试器引擎的实例并连接到进程服务器。 该方法[ **ConnectProcessServer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-connectprocessserver)将连接到进程服务器。 一次连接中所述的方法[Live 用户模式目标](live-user-mode-targets.md)可用。

完成与进程服务器远程客户端时，它可以断开连接，使用[ **DisconnectProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-disconnectprocessserver)，或者可以使用[ **EndProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-endprocessserver)请求进程服务器关闭。 若要关闭的情况下从计算机上运行的进程服务器，请使用任务管理器结束进程。 如果使用调试器的实例引擎**StartProcessServer**仍在运行，它可以使用[ **Execute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-execute)发出调试器命令[ **.endsrv 0**](-endsrv--end-debugging-server-.md)，以将结束进程服务器 (这是常用的行为的异常 **.endsrv**，这通常不会影响的进程服务器)。

进程服务器和智能客户端之间的通信通常包含内存、 处理器和操作系统的低级操作和从远程客户端发送到服务器的请求。 其结果随后会发送回客户端。

 

 





