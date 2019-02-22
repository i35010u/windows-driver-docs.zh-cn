---
title: 远程调试过程中的安全性
description: 远程调试过程中的安全性
ms.assetid: 55e570d2-b005-4c09-ac8f-0632233a64bd
keywords:
- 安全注意事项，远程调试
- 远程调试通过 remote.exe，安全注意事项
- 远程调试执行调试程序的安全注意事项
- 进程服务器的安全注意事项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d0ac7750e8e69100b9ac45c24d4dc21f3ffd64e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543258"
---
# <a name="security-during-remote-debugging"></a>远程调试过程中的安全性


## <span id="ddk_security_during_remote_debugging_dbg"></span><span id="DDK_SECURITY_DURING_REMOTE_DEBUGGING_DBG"></span>


有两种方法来远程调试过程中提高安全： 限制谁可以连接到你的会话以及限制整理的人 does 连接。

### <a name="span-idcontrollingaccesstothedebuggingsessionspanspan-idcontrollingaccesstothedebuggingsessionspancontrolling-access-to-the-debugging-session"></a><span id="controlling_access_to_the_debugging_session"></span><span id="CONTROLLING_ACCESS_TO_THE_DEBUGGING_SESSION"></span>控制对调试会话的访问

如果您正在执行[通过在调试器的远程调试](remote-debugging-through-the-debugger.md)，或使用[进程服务器](process-servers--user-mode-.md)或[KD 连接服务器](kd-connection-servers--kernel-mode-.md)，可以尝试在本地网络上的任何计算机将附加到调试会话。

如果正在使用 TCP，1394，COM，或命名管道协议，可能需要调试客户端提供一个密码。 但是，此密码未加密期间传输，并且因此这些协议不安全。

如果你想让调试服务器安全，必须使用安全套接字层 (SSL) 或安全管道 (SPIPE) 协议。

如果您正在执行[remote.exe 通过远程调试](remote-debugging-through-remote-exe.md)，可以使用 **/u**参数来禁止未经授权的用户的连接。

### <a name="span-idrestrictingthepowersoftheclientspanspan-idrestrictingthepowersoftheclientspanrestricting-the-powers-of-the-client"></a><span id="restricting_the_powers_of_the_client"></span><span id="RESTRICTING_THE_POWERS_OF_THE_CLIENT"></span>限制客户端的幂

如果您设置了内核模式调试会话，可以限制干扰主机使用的调试器的能力[安全模式下](secure-mode.md)。

在用户模式下，安全模式下不可用。 你可以停止的侵入性的客户端从发出 Microsoft MS-DOS 命令和运行外部程序通过发出[ **.noshell （禁止 Shell 命令）** ](-noshell--prohibit-shell-commands-.md)命令。 但是，有许多其他方法会影响您的计算机的客户端。

请注意，这两种安全模式和 **.noshell**将阻止调试客户端和调试服务器执行某些操作。 没有方法在客户端上，但是服务器上放置限制。

### <a name="span-idforgottenprocessserversspanspan-idforgottenprocessserversspanforgotten-process-servers"></a><span id="forgotten_process_servers"></span><span id="FORGOTTEN_PROCESS_SERVERS"></span>忘记了的进程服务器

在远程计算机上启动的进程服务器，进程服务器会以无提示方式运行。

如果执行远程调试，通过此进程服务器，然后结束会话的进程服务器将继续运行。

忘记了的进程服务器是一种攻击的潜在目标。 始终应关闭不需要的进程服务器。 使用任务管理器中的 Kill.exe 实用工具终止进程服务器。

 

 





