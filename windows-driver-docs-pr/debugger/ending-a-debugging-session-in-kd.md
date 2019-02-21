---
title: 结束调试会话中 KD
description: 结束调试会话中 KD
ms.assetid: 6CD39971-424D-4F29-9A36-CCD14187DEB0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d114286fd8ebfc1e2f2bfe8e8eeba0a255c7586
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544328"
---
# <a name="ending-a-debugging-session-in-kd"></a>结束调试会话中 KD


有两种不同方式退出 KD。

-   问题[ **q (Quit)** ](q--qq--quit-.md) KD 保存日志文件、 结束调试会话并退出调试器命令。 目标计算机保持锁定状态。

-   按[ **CTRL + B** ](ctrl-b--quit-local-debugger-.md)然后按 ENTER 以结束调试程序突然。 如果你想在目标计算机继续运行调试程序结束后，必须使用此方法。 CTRL + B 不会删除断点，因为您应首先使用以下命令。

    ```dbgcmd
    kd>  bc *
    kd>  g
    ```

通过使用 CTRL + B 退出调试器并不会清除内核模式断点，但附加新的内核调试程序 does 清除这些断点。

执行远程调试时[ **q** ](q--qq--quit-.md)结束调试会话。 CTRL + B 退出调试器，但将该会话活动。 这种情况下使另一个调试器能够连接到该会话。

如果[ **q (Quit)** ](q--qq--quit-.md)命令不起作用，请按[ **CTRL + R** ](ctrl-r--re-synchronize-.md) ，然后主计算机的键盘上按 ENTER，然后重试**q**命令。 如果此过程不会起作用，则必须使用 CTRL + B 退出调试器。

 

 





