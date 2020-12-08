---
title: 远程调试期间的安全性
description: 远程调试期间的安全性
keywords:
- 安全注意事项，远程调试
- 通过 remote.exe 远程调试，安全注意事项
- 通过调试器进行远程调试，安全注意事项
- 进程服务器，安全注意事项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d785e5b5db50a6fd29f0300ac25660f6bdd0578
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786925"
---
# <a name="security-during-remote-debugging"></a>远程调试期间的安全性


## <span id="ddk_security_during_remote_debugging_dbg"></span><span id="DDK_SECURITY_DURING_REMOTE_DEBUGGING_DBG"></span>


在远程调试过程中，有两种方法可以提高安全性：通过限制可连接到会话的人员，以及限制连接的人员的使用权限。

### <a name="span-idcontrolling_access_to_the_debugging_sessionspanspan-idcontrolling_access_to_the_debugging_sessionspancontrolling-access-to-the-debugging-session"></a><span id="controlling_access_to_the_debugging_session"></span><span id="CONTROLLING_ACCESS_TO_THE_DEBUGGING_SESSION"></span>控制对调试会话的访问

如果要 [通过调试器执行远程调试](remote-debugging-through-the-debugger.md)，或使用 [进程服务器](process-servers--user-mode-.md) 或 [KD 连接服务器](kd-connection-servers--kernel-mode-.md)，则本地网络上的任何计算机都可以尝试附加到您的调试会话。

如果使用的是 TCP、1394、COM 或命名管道协议，则可以要求调试客户端提供密码。 但是，在传输过程中不会对此密码进行加密，因此这些协议不安全。

如果希望调试服务器是安全的，则必须使用安全套接字层 (SSL) 或安全管道 (SPIPE) 协议。

如果 [通过 remote.exe执行远程调试](remote-debugging-through-remote-exe.md)，则可以使用 **/u** 参数禁止未经授权的用户进行连接。

### <a name="span-idrestricting_the_powers_of_the_clientspanspan-idrestricting_the_powers_of_the_clientspanrestricting-the-powers-of-the-client"></a><span id="restricting_the_powers_of_the_client"></span><span id="RESTRICTING_THE_POWERS_OF_THE_CLIENT"></span>限制客户端的电源

如果要设置内核模式调试会话，则可以使用 [安全模式](secure-mode.md)限制调试器干扰主机计算机的能力。

在用户模式下，安全模式不可用。 你可以通过发出 [**. noshell (禁用 Shell 命令)**](-noshell--prohibit-shell-commands-.md) 命令来阻止干扰性客户端发出 Microsoft MS-DOS 命令和运行外部程序。 但是，有许多其他方法可让客户端干扰您的计算机。

请注意，安全模式和 **noshell** 都会阻止调试客户端和调试服务器执行特定操作。 无法在客户端上设置限制，而不是在服务器上进行限制。

### <a name="span-idforgotten_process_serversspanspan-idforgotten_process_serversspanforgotten-process-servers"></a><span id="forgotten_process_servers"></span><span id="FORGOTTEN_PROCESS_SERVERS"></span>忘记的进程服务器

在远程计算机上启动进程服务器时，进程服务器将以无提示方式运行。

如果通过此进程服务器执行远程调试，然后结束会话，进程服务器将继续运行。

忘记的进程服务器是攻击的潜在目标。 应始终关闭不需要的进程服务器。 使用 Kill.exe 实用工具或任务管理器终止进程服务器。

 

 





