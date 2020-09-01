---
title: 自动调试服务应用程序
description: 自动调试服务应用程序
ms.assetid: 3168b5c1-30fa-4ff5-b871-736dcdeb8f31
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 423b004ad91ab68e0c505a1fe9aa94c978c6a714
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212587"
---
# <a name="debugging-the-service-application-automatically"></a>自动调试服务应用程序


启动服务应用程序时，可以自动启动调试器。 或者，它可以在服务应用程序遇到异常或执行 **DebugBreak** 命令时自动启动。 如果你选择了其中一种方法，本主题将说明如何继续。 如果不确定选择哪种方法，请参阅 [选择最佳方法](choosing-the-best-method.md)。

然后使用以下过程：

1.  执行以下准备步骤之一：
    -   如果打算从头开始调试服务应用程序（包括其初始化代码），请按照启用初始化代码调试中所述的过程进行操作。 或者，如果你希望服务应用程序在崩溃或遇到异常时进入调试器，请按照使服务应用程序中断到调试器中所述的过程进行操作。
    -   若要确保服务应用程序允许调试器正常运行，请执行 [调整服务应用程序超时](preparing-to-debug-the-service-application.md#adjusting-the-service-application-timeout)中所述的过程。
    -   如果服务与单个 SvcHost 进程中的其他服务结合使用，则执行隔离服务中所述的过程。

2.  如果服务已在运行，则必须重新启动才能使这些更改生效。 为了消除正在运行的服务的任何影响，我们建议您重新启动 Windows 本身。 如果你不想重新启动 Windows，请使用以下命令，其中 *ServiceName* 是服务的名称：

    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

3.  如果已选择调试服务应用程序的初始化代码，则在服务启动时，调试器将启动并附加到服务应用程序。

    如果选择让调试器触发异常，则服务应用程序会在遇到异常或执行 **DebugBreak** 函数之前正常执行。 此时，调试器将启动并附加到服务应用程序。

4.  下一步取决于你在步骤1中指定的调试程序命令行：
    -   如果在没有任何远程处理选项的情况下指定了调试程序，则将启动此调试器并显示其窗口。
    -   如果使用-server 和-noio 选项指定了 NTSD，则将在没有控制台窗口的情况下启动 NTSD。 然后，可以通过使用-remote 参数启动任何用户模式调试器，从另一台计算机连接到调试会话。 有关说明，请参阅 [**激活调试客户端**](activating-a-debugging-client.md)。
    -   如果使用-d 选项指定了 NTSD，则在没有控制台窗口的情况下启动 NTSD。 然后，你可以通过使用在另一台计算机上运行的内核调试器连接到调试会话。 有关说明，请参阅 [从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。
    -   如果使用-ddefer 和-server 选项指定了 NTSD，则将在没有控制台窗口的情况下启动 NTSD。 然后，你可以通过使用内核调试器和用户模式远程调试器来连接到调试会话，该调试器在不同于服务 (的计算机上运行，但可能与每个其他计算机) 相同。 有关说明，请参阅 [结合此方法与远程调试](combining-this-method-with-remote-debugging.md)。

5.  调试器启动时，服务在初始进程断点、异常或 **DebugBreak** 命令处暂停。 这使您可以检查服务应用程序的当前状态，设置断点，并进行任何其他所需的配置选择。

6.  使用 [**g (中转) **](g--go-.md) 或其他执行命令继续执行服务应用程序。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[DebugBreak 函数](/windows/win32/api/debugapi/nf-debugapi-debugbreak)

 

