---
title: 在 KD 中结束调试会话
description: 在 KD 中结束调试会话
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72fd901ea59404c0d200b8d1fdc0a0aa94cf8490
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820921"
---
# <a name="ending-a-debugging-session-in-kd"></a>在 KD 中结束调试会话


可以通过两种不同的方式退出 KD。

-   发出 [**q (Quit)**](q--qq--quit-.md) KD 中的命令以保存日志文件、结束调试会话并退出调试器。 目标计算机保持锁定状态。

-   按 [**CTRL + B**](ctrl-b--quit-local-debugger-.md) ，然后按 enter 键，使调试器突然结束。 如果希望目标计算机在调试器结束后继续运行，则必须使用此方法。 由于 CTRL + B 并不删除断点，因此应该首先使用以下命令。

    ```dbgcmd
    kd>  bc *
    kd>  g
    ```

使用 CTRL + B 退出调试器并不清除内核模式断点，但附加新的内核调试器会清除这些断点。

执行远程调试时， [**q**](q--qq--quit-.md) 会结束调试会话。 CTRL + B 退出调试器，但使会话保持活动状态。 这种情况下，另一个调试器可以连接到该会话。

如果 [**q (Quit)**](q--qq--quit-.md) 命令不起作用，请按 [**CTRL + R**](ctrl-r--re-synchronize-.md) ，然后在主计算机的键盘上按 enter，然后重试 **q** 命令。 如果此过程不起作用，则必须使用 CTRL + B 退出调试器。

 

 





