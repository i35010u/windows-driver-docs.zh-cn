---
title: 远程调试
description: 本主题提供远程用户模式下调试的概述。 这涉及到两台计算机，客户端和服务器。
ms.assetid: fa87b55c-c339-4b8c-8614-c7355d203a6e
keywords: 远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ba57a1b7b9e4eac7afecc441991ab3963a5590d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540827"
---
# <a name="remote-debugging"></a>远程调试


## <span id="ddk_remote_debugging_dbg"></span><span id="DDK_REMOTE_DEBUGGING_DBG"></span>


远程用户模式下调试涉及两台计算机：*客户端*并*server*。 服务器是运行要调试的应用程序的计算机。 用户模式下调试程序或进程服务器，还在运行服务器。 客户端是远程控制调试会话的计算机。

内核模式远程调试涉及三台计算机：*客户端*，则*服务器*，并*目标计算机*。 目标计算机是要调试的计算机。 服务器是运行内核调试程序或 KD 连接服务器的计算机。 客户端是远程控制调试会话的计算机。

[选择最佳的远程调试方法](choosing-the-best-remote-debugging-method.md)

[通过在调试器的远程调试](remote-debugging-through-the-debugger.md)

[控制用户模式下的调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)

[远程调试通过 Remote.exe](remote-debugging-through-remote-exe.md)

[进程服务器 （用户模式）](process-servers--user-mode-.md)

[KD 连接服务器 （内核模式）](kd-connection-servers--kernel-mode-.md)

[重复字符](repeaters.md)

[高级远程调试方案](advanced-remote-debugging-scenarios.md)

[在工作组计算机上进行远程调试](remote-debugging-on-workgroup-computers.md)

 

 





