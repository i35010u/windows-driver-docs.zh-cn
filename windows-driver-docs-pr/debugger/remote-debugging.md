---
title: 远程调试
description: 本主题提供远程用户模式调试的概述。 这涉及到两台计算机的客户端和服务器。
keywords: 远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1daaccc5ce466d66787d9e6ea90167703d77c99e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831933"
---
# <a name="remote-debugging"></a>远程调试


## <span id="ddk_remote_debugging_dbg"></span><span id="DDK_REMOTE_DEBUGGING_DBG"></span>


远程用户模式调试涉及两台计算机： *客户端* 和 *服务器*。 服务器是运行要调试的应用程序的计算机。 服务器还运行用户模式调试器或进程服务器。 客户端是远程控制调试会话的计算机。

远程内核模式调试涉及三台计算机： *客户端*、 *服务器* 和 *目标计算机*。 目标计算机是要调试的计算机。 服务器是运行内核调试器或 KD 连接服务器的计算机。 客户端是远程控制调试会话的计算机。

[选择最佳的远程调试方法](choosing-the-best-remote-debugging-method.md)

[通过调试器进行远程调试](remote-debugging-through-the-debugger.md)

[通过内核调试程序控制用户模式调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)

[通过 Remote.exe 进行远程调试](remote-debugging-through-remote-exe.md)

[进程服务器（用户模式）](process-servers--user-mode-.md)

[KD 连接服务器（内核模式）](kd-connection-servers--kernel-mode-.md)

[中继器](repeaters.md)

[高级远程调试方案](advanced-remote-debugging-scenarios.md)

[在工作组计算机上进行远程调试](remote-debugging-on-workgroup-computers.md)

 

 





