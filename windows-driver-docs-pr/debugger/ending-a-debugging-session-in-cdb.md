---
title: 结束调试会话中 CDB
description: 可以通过输入 q (Quit) 命令来退出 CDB。 此命令也会关闭正在调试的应用程序。
ms.assetid: B32AD09D-7F88-420E-94BD-59FAE6EC1720
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60741484442d6e66411251968fbc88af001a412c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519801"
---
# <a name="ending-a-debugging-session-in-cdb"></a>结束调试会话中 CDB


可以通过输入退出 CDB [ **q (Quit)** ](q--qq--quit-.md)命令。 此命令也会关闭正在调试的应用程序。

[ **Qd （Quit 和分离）** ](qd--quit-and-detach-.md)命令，从目标应用程序中分离 CDB、 退出调试器，并保持运行的目标应用程序。 如果您使用了 **-pd**如果出于任何原因终止会话，则会出现在启动调试器，分离时的命令行选项。 (此技术使得 **-pd**调试敏感的进程，如客户端服务器运行时子系统 (CSRSS)，您不想要结束时尤其有用。)

如果调试器未响应，可以通过按退出[ **CTRL + B** ](ctrl-b--quit-local-debugger-.md) ，然后输入。 此方法是辅助退出机制。 它突然结束调试器，它类似于结束进程通过任务管理器或关闭窗口。

若要结束用户模式下调试会话，请返回到休眠模式下，调试器和关闭目标应用程序，可以使用以下方法：

-   输入[ **.kill （终止进程）** ](-kill--kill-process-.md)命令。

若要结束用户模式下调试会话，请为休眠模式中，并再次运行目标应用程序的情况下，可以使用以下方法将返回调试器：

-   输入[ **.detach （与进程分离）** ](-detach--detach-from-process-.md)命令。 如果你正在调试多个目标，此命令将当前目标从分离，并将剩余目标的调试会话继续。

-   输入[ **qd （Quit 和分离）** ](qd--quit-and-detach-.md)命令。

-   输入[ **q (Quit)** ](q--qq--quit-.md)命令时，如果启动的调试器 **-pd**选项。

若要用户模式下调试会话结束，返回调试器到休眠模式，但使目标应用程序处于调试状态，可以使用以下方法：

-   输入[ **.abandon （放弃进程）** ](-abandon--abandon-process-.md)命令。

有关重新附加到目标的详细信息，请参阅[重新附加到目标应用程序](reattaching-to-the-target-application.md)。

 

 





