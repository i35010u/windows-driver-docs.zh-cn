---
title: 在 CDB 中结束调试会话
description: 可以通过输入 q (Quit) 命令退出 CDB。 此命令还会关闭正在调试的应用程序。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 137bd6156a91fc7af406859d9fdbc3fbab2ad9ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820923"
---
# <a name="ending-a-debugging-session-in-cdb"></a>在 CDB 中结束调试会话


可以通过输入 [**q (Quit)**](q--qq--quit-.md) 命令退出 CDB。 此命令还会关闭正在调试的应用程序。

[**Qd (退出并分离)**](qd--quit-and-detach-.md)命令从目标应用程序分离 CDB，退出调试器，并使目标应用程序保持运行。 如果在启动调试器时使用了 **-pd** 命令行选项，则在会话出于任何原因结束时，将发生分离。  (在调试敏感进程（例如客户端服务器 Run-Time 子系统 (CSRSS) ）时，此方法 **会特别有用** ，因为您不希望结束。 ) 

如果调试器未响应，可以按 [**CTRL + B**](ctrl-b--quit-local-debugger-.md) 退出，然后按 enter。 此方法是一种辅助退出机制。 它突然结束调试器，类似于通过任务管理器或通过关闭窗口来结束进程。

若要结束用户模式调试会话，请将调试器返回到休眠模式，然后关闭目标应用程序，可以使用以下方法：

-   输入 [**kill (Kill Process)**](-kill--kill-process-.md) 命令。

若要结束用户模式调试会话，请将调试器返回到休眠模式，然后将目标应用程序设置为再次运行，可以使用以下方法：

-   输入 [**(从进程中分离的)**](-detach--detach-from-process-.md) "命令。 如果正在调试多个目标，则此命令从当前目标中分离，并继续与剩余目标的调试会话。

-   输入 [**qd (Quit 并分离)**](qd--quit-and-detach-.md) 命令。

-   如果已通过 **-pd** 选项启动调试器，请输入 [**q (Quit)**](q--qq--quit-.md)命令。

若要结束用户模式调试会话，请将调试器恢复到休眠模式，但使目标应用程序处于调试状态，可以使用以下方法：

-   输入 [**(放弃进程)**](-abandon--abandon-process-.md) 命令。

有关重新附加到目标的详细信息，请参阅重新 [附加到目标应用程序](reattaching-to-the-target-application.md)。

 

 





