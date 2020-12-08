---
title: 与目标计算机同步
description: 与目标计算机同步
keywords:
- 与目标计算机同步
- 与目标计算机同步，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74f219da19904e48944a9342d2912a1aad04c8eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813919"
---
# <a name="synchronizing-with-the-target-computer"></a>与目标计算机同步


## <span id="ddk_synchronizing_with_the_target_computer_dbg"></span><span id="DDK_SYNCHRONIZING_WITH_THE_TARGET_COMPUTER_DBG"></span>


有时，在内核模式调试期间，目标计算机停止响应调试器。

在 KD 中，可以按 [**CTRL + R (重新同步)**](ctrl-r--re-synchronize-.md) 然后按 enter 与目标计算机同步。 在 WinDbg 中，使用 [CTRL + ALT + R](debug---kernel-connection---resynchronize.md) 或 Debug |内核连接 |重新同步.

这些命令经常还原主机与目标之间的通信。 但是，重新同步可能并不总是成功，尤其是在使用1394内核连接的情况下。

请 [**重新启动 (Restart 内核连接)**](-restart--restart-kernel-connection-.md) 命令提供更强大的重新同步方法。 此命令等效于退出调试器，然后将新的调试器附加到现有会话。 此命令仅在 KD 中可用，不能在 WinDbg 中使用。

[通过 remote.exe执行远程调试](remote-debugging-through-remote-exe.md)时， **restart** 命令最有用。  (这种调试中，可能很难结束并重新启动调试器。 ) 不过，如果您是通过调试器执行远程调试，则不能使用. 从调试客户端 **重新启动** 。

 

 





