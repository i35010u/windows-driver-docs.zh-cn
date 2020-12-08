---
title: 将此方法与远程调试结合使用
description: 将此方法与远程调试结合使用
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7cc71a38fa6aa3bfbf9333efb3f292e8a0040b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831983"
---
# <a name="combining-this-method-with-remote-debugging"></a>将此方法与远程调试结合使用


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


有时， [从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)并同时将用户模式调试器用作 [调试服务器](remote-debugging-through-the-debugger.md) 很有用。

例如，当用户模式符号位于符号服务器上时，此配置非常有用。 在用于从内核调试器控制用户模式调试器的标准配置中，这两个调试器的交互可能会导致同步的微小中止，并且这些失误会阻止符号服务器身份验证。 此处所述的更为复杂的配置可以避免此问题。

**注意**   在描述此方案时， *目标应用程序* 是指正在调试的用户模式应用程序， *目标计算机* 指的是包含目标应用程序的计算机和 CDB 或 NTSD 进程， *主机计算机* 指的是包含内核调试器的计算机。

 

若要使用此方法，必须执行以下操作：

1.  在目标计算机上启动 NTSD 或 CDB，其中包含-ddefer 和-server 命令行选项，并指定所需的传输选项。 -Server 选项必须是命令行中的第一个参数。

    例如，可以使用以下语法附加到正在运行的进程。

    ```console
    ntsd -server ServerTransport -ddefer [-y UserSymbolPath] -p PID 
    ```

    或者，您可以使用以下语法作为目标来启动一个新进程。

    ```console
    ntsd -server ServerTransport -ddefer [-y UserSymbolPath] ApplicationName 
    ```

    如果要将此安装为事后调试器，请使用以下语法。 请注意，必须手动编辑注册表才能安装包含-server 参数的事后调试器，有关详细信息，请参阅 [启用事后调试](enabling-postmortem-debugging.md)。

    ```console
    ntsd -server ServerTransport -ddefer [-y UserSymbolPath] 
    ```

    有关可用传输选项的详细信息，请参阅 [**激活调试服务器**](activating-a-debugging-server.md)。

2.  在主计算机上启动 WinDbg 或 KD，就像打算调试目标计算机一样，但实际上不会中断目标计算机。 若要使用 WinDbg，请使用以下语法。

    ```console
    windbg [-y KernelSymbolPath] [-k ConnectionOptions] 
    ```

    有关此步骤的详细信息，请参阅 [使用 WinDbg 进行实时 Kernel-Mode 调试](performing-kernel-mode-debugging-using-windbg.md)

    .

3.  使用与启动服务器相同的传输选项，启动 WinDbg 或 CDB 作为调试客户端。 此调试客户端可以在主计算机上运行，也可以在第三台计算机上运行。

    ```console
    cdb -remote ClientTransport 
    ```

    有关此步骤的详细信息，请参阅 [**激活调试客户端**](activating-a-debugging-client.md)。

4.  运行完调试器并在 `Input>` 内核调试器中显示提示后，请使用 " [**睡眠 (pause 调试器")**](-sleep--pause-debugger-.md) 命令暂停调试器，并让目标计算机运行几秒钟时间。 这使目标计算机能够处理远程传输协议，从而建立用户模式远程服务器与远程客户端之间的连接。

如果使用 CDB 作为用户模式调试器，则与 CDB 关联的命令提示符窗口将保持锁定状态，并且在调试继续时不可用。 如果使用 NTSD，则不会创建任何其他窗口，即使 NTSD 在目标计算机上具有与之关联的进程 ID。

在此组合方案中，在此组合方案中所述的四种模式 [和切换方法](switching-modes.md) 在此组合方案中所述，具有以下差异：

-   用户模式调试模式有两种不同的模式。 当目标计算机运行时，调试服务器由调试客户端控制，就像在任何其他远程调试会话中一样。这称为 *远程控制用户模式调试*。 如果将内核模式调试器中断到目标计算机并 `Input>` 显示提示，则用户模式调试器由内核调试器控制; 这称为 *内核控制的用户模式调试*。

-   这两种模式绝不会同时可用。 如果将内核调试器分成目标计算机，即使用户模式调试器可能处于活动状态，目标计算机也无法处理远程传输协议，因此，用户模式调试器将无法跨此连接接收远程输入。

-   如果用户模式符号位于某个符号服务器上，则在远程控制的用户模式调试模式下，应发出要求符号访问的任何调试器命令。

-   若要从内核控制的用户模式调试切换到远程控制的用户模式调试，请使用 " [**睡眠 (暂停调试器")**](-sleep--pause-debugger-.md) 命令。 当用户模式调试器从睡眠命令唤醒时，它将处于远程控制的用户模式调试模式。

-   若要从远程控制的用户模式调试切换到内核模式调试，请在提示符下输入命令 `Input>` 。 如果未显示此提示，请切换到内核模式调试，然后在提示符处使用 [**g (中转)**](g--go-.md) 命令 `kd>` 。

在内部，用户模式调试器从-ddefer 开始向调试客户端提供第一个优先级，第二个优先级为内核调试器输入。 但是，并发输入之间永远不会发生冲突，因为当内核调试器已在目标计算机中出现故障时，远程连接将不可用。

 

 





