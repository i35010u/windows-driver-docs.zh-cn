---
title: 将此方法与远程调试结合使用
description: 将此方法与远程调试结合使用
ms.assetid: 4f9a60ab-b221-4a60-b3d5-cd907e33ec19
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba4ac0f24818d621af9580d54fff0559721fbccd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375081"
---
# <a name="combining-this-method-with-remote-debugging"></a>将此方法与远程调试结合使用


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


有时是有益的[控制用户模式下的调试程序与内核调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)，使用作为用户模式下的调试[调试服务器](remote-debugging-through-the-debugger.md)在同一时间。

例如，此配置非常有用，当用户模式符号位于符号服务器上。 标准配置中用于控制用户模式下的调试程序与内核调试程序，这两个交互调试器可能会导致在同步中，很小的超时期结束，这些超时期结束可以阻止符号服务器身份验证。 此处所述的更复杂配置可以避免此问题。

**请注意**  中描述此方案中，*应用程序的目标*正在调试的用户模式应用程序是指*目标计算机*指的计算机，包含目标应用程序和 CDB 或 NTSD 过程，并*主机计算机*指包含内核调试程序的计算机。

 

若要使用此方法，必须执行以下操作：

1.  NTSD 或 CDB 启动具有-ddefer 和服务器的命令行选项，指定所需的传输选项的目标计算机上。 -Server 选项必须为命令行上的第一个参数。

    例如，您可以将附加到正在运行的进程使用以下语法。

    ```console
    ntsd -server ServerTransport -ddefer [-y UserSymbolPath] -p PID 
    ```

    或者，可以通过使用以下语法为目标中开始一个新的进程。

    ```console
    ntsd -server ServerTransport -ddefer [-y UserSymbolPath] ApplicationName 
    ```

    如果您正在安装这作为事后调试程序，将使用以下语法。 请注意，必须手动编辑注册表，以安装包括事后调试器-server 参数;有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

    ```console
    ntsd -server ServerTransport -ddefer [-y UserSymbolPath] 
    ```

    有关可用的传输选项的信息，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。

2.  启动的 WinDbg 或 KD 的主机计算机上，好像要调试的目标计算机，但不是实际会中断到目标计算机。 若要使用 WinDbg，请使用以下语法。

    ```console
    windbg [-y KernelSymbolPath] [-k ConnectionOptions] 
    ```

    有关此步骤的详细信息，请参阅[Live 内核模式调试使用 WinDbg](performing-kernel-mode-debugging-using-windbg.md)

    .

3.  使用相同的传输选项用于启动服务器，以调试客户端，启动 WinDbg 或 CDB。 主计算机上或第三个计算机上，可以运行此调试客户端。

    ```console
    cdb -remote ClientTransport 
    ```

    有关此步骤的详细信息，请参阅[**激活调试客户端**](activating-a-debugging-client.md)。

4.  运行调试程序后，`Input>`提示将显示在内核调试器中，使用[ **.sleep （暂停调试器）** ](-sleep--pause-debugger-.md)命令暂停调试器，并允许目标计算机运行的几个秒数。 这样，处理远程传输协议，在用户模式下远程服务器和远程客户端之间建立连接的目标计算机时间。

如果您使用 CDB 作为用户模式下调试程序，与 CDB 相关联的命令提示符窗口锁定并且不可用时保持调试将继续。 如果使用 NTSD，被创建没有其他窗口，即使 NTSD 具有与之关联的目标计算机上的进程 ID。

四种模式和方法的主题中介绍它们之间进行切换[切换模式](switching-modes.md)应用在此组合方案中，存在以下差异：

-   有两种不同的用户模式下调试模式。 当目标计算机运行时，由与任何其他远程调试会话; 调试客户端控制调试服务器这称为*受远程控制用户模式下调试*。 到目标计算机以破坏内核模式调试程序时，`Input>`显示提示，由内核调试器控制用户模式下调试程序; 这称为*内核控制用户模式下调试*。

-   在同一时间是永远不会提供这两种模式。 如果内核调试器中断到目标计算机，即使用户模式下调试程序可以处于活动状态，目标计算机将无法处理远程传输协议，并因此用户模式下调试程序将无法再接收跨远程输入此连接。

-   如果您的用户模式符号位于符号服务器上，应受远程控制用户模式下调试模式中发出任何调试器命令需要符号访问权限。

-   若要从内核控制用户模式下调试远程控制用户模式下调试切换，请使用[ **.sleep （暂停调试器）** ](-sleep--pause-debugger-.md)命令。 当用户模式下调试程序唤醒从睡眠状态命令时，将在远程控制用户模式下调试模式下。

-   若要从远程控制用户模式下调试到内核模式调试切换，请输入从任何命令`Input>`提示符。 如果此提示不可见，请切换到内核模式调试中，，然后使用[ **g （转向）** ](g--go-.md)命令在`kd>`提示符。

在内部，用户模式下调试程序入门-ddefer 可提供最优先的任务输入调试客户端和第二个输入从内核调试程序的优先级。 但是，可以永远不会有冲突之间同时输入，因为内核调试程序损坏到目标计算机，将无法远程连接。

 

 





