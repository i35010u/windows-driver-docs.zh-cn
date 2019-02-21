---
title: 自动调试服务应用程序
description: 自动调试服务应用程序
ms.assetid: 3168b5c1-30fa-4ff5-b871-736dcdeb8f31
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2155fbf040a18ec4e7036ffd8ff8793918aecc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526526"
---
# <a name="debugging-the-service-application-automatically"></a>自动调试服务应用程序


服务应用程序启动时，可以自动启动调试器。 或者，它可以自动时启动的服务应用程序遇到的异常或执行**DebugBreak**命令。 如果选择了下列方法之一后，本主题说明如何继续。 如果不确定要选择哪种方法，请参阅[选择最佳方法](choosing-the-best-method.md)。

然后使用以下过程：

1.  执行下列预备步骤操作：
    -   如果你打算调试服务应用程序从一开始，包括其初始化代码，并按照启用调试初始化代码中所述的过程。 此外，如果你想要在发生故障或遇到的异常时中断调试器服务应用程序，按照使服务应用程序到中断到调试器中所述的过程。
    -   若要确保服务应用程序将允许调试器正常运行，执行过程中所述[调整服务应用程序超时](preparing-to-debug-the-service-application.md#adjusting-the-service-application-timeout)。
    -   如果该服务与单个 SvcHost 进程中的其他服务结合使用，执行隔离服务中所述的过程。

2.  如果该服务已运行，必须重新启动它做的更改才会生效。 我们建议以删除正在运行的服务的任何影响 Windows 本身，重新启动。 如果您不想要重新启动 Windows，使用以下命令，其中*ServiceName*是服务名称：

    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

3.  如果您在服务启动时调试服务应用程序的初始化代码，调试器将启动，并将附加到服务应用程序。

    如果您已选择使调试器可以由异常触发，服务应用程序正常执行直到它遇到的异常或执行**DebugBreak**函数。 在此情况下，调试器将启动，并将附加到服务应用程序。

4.  下一步取决于你在步骤 1 中指定的调试器命令行：
    -   如果指定不使用任何远程处理选项调试器，启动此调试程序和其窗口变得可见。
    -   如果指定 NTSD 使用-server 和-noio 选项，NTSD 启动不在控制台窗口。 您然后可以连接到调试会话从另一台计算机通过启动任何用户模式下使用-远程参数调试器。 有关说明，请参阅[**激活调试客户端**](activating-a-debugging-client.md)。
    -   如果使用-d 选项指定 NTSD，则将不在控制台窗口启动 NTSD。 通过使用另一台计算机上运行的内核调试程序，可以再连接到调试会话。 有关说明，请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。
    -   如果使用-ddefer 和服务器选项指定 NTSD，NTSD 被启动不在控制台窗口。 通过使用内核调试程序和用户模式下远程调试器，不同于服务的计算机 （但可能是为每个其他在同一台计算机） 上运行，可以再连接到调试会话。 有关说明，请参阅[结合使用远程调试的此方法](combining-this-method-with-remote-debugging.md)。

5.  当调试器启动时，初始过程断点，该异常，在服务暂停或**DebugBreak**命令。 这使您检查服务应用程序的当前状态、 设置断点，并进行任何其他所需的配置选择。

6.  使用[ **g （转向）** ](g--go-.md)或另一个执行命令来恢复服务应用程序的执行。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[DebugBreak 函数](https://go.microsoft.com/fwlink/p/?linkid=124229)

 

 






