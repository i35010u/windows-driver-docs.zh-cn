---
title: 选择最佳的远程调试方法
description: 选择最佳的远程调试方法
keywords:
- 远程调试，选择最佳方法
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ad6c8b09b511ef17eec18ea7f1457ab78ecd29c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821607"
---
# <a name="choosing-the-best-remote-debugging-method"></a>选择最佳的远程调试方法


## <span id="ddk_choosing_the_best_remote_debugging_method_dbg"></span><span id="DDK_CHOOSING_THE_BEST_REMOTE_DEBUGGING_METHOD_DBG"></span>


可以使用两种主要方法来执行远程调试，还可以使用多种方法和大量组合方法。

下面是一些提示，可帮助你选择最佳方法。

-   [通过调试器进行远程调试](remote-debugging-through-the-debugger.md) 通常是最佳方法。 如果你只是有一台服务器和一台客户端可以自由地相互连接，则在客户端和服务器上都安装了相同的调试器二进制文件，并且将运行客户端的调试技术人员将能够与服务器在房间内与服务器通信，这是建议的方法。

    客户端和服务器可以运行任何版本的 Windows。 它们不必彼此运行相同的版本。

    如果客户端无法将连接请求发送到服务器，但服务器可以向客户端发送请求，则可以通过使用 **clicon** 参数通过使用 *反向连接* 的调试器来使用远程调试。

-   [通过 remote.exe进行远程调试 ](remote-debugging-through-remote-exe.md) 用于远程控制命令提示符窗口。 它可用于远程控制 KD、CDB 或 NTSD。 不能与 WinDbg 一起使用。

    如果客户端没有调试器二进制文件的副本，则必须使用 remote.exe 方法。

-   如果调试技术人员将无法与服务器房间中的某人通信，则可以使用 **进程服务器** 或 **KD 连接服务器**。 所有实际的调试工作都是由 (称为 *智能客户端*) 的客户端进行的;这样就无需在服务器本身显示第二人。

    进程服务器用于用户模式调试;KD 连接服务器用于内核模式调试。 除了这种区别以外，它们的行为方式类似。

    如果运行服务器的计算机不能处理大量的进程负载，或者运行客户端的技术人员有权访问机密且无法由服务器访问的符号文件或源文件，此方法也非常有用。 但是，与通过调试器进行远程调试相比，此方法的速度更快或效率更高。 此方法不能用于转储文件调试。

    有关详细信息，请参阅 [进程服务器 (用户模式) ](process-servers--user-mode-.md) 和 [KD 连接服务器 (内核模式) ](kd-connection-servers--kernel-mode-.md) 。

-   **中继器** 是在两台计算机之间中继数据的轻型代理服务器。 如果通过调试器执行远程调试或使用进程服务器，则可以在客户端与服务器之间添加中继器。

    如果客户端和服务器无法直接相互通信，但可以访问外部计算机，则可能需要使用中继器。 也可以结合使用反向连接与中继器。 甚至可以在一行中使用两个中继器，但这种情况很少需要。

    请参阅 [中继器](repeaters.md) 获取详细信息。

-   还可以从内核调试器控制 CDB (或 NTSD) 。 这是另一种形式的远程调试。 有关详细信息，请参阅 [控制内核调试器中的 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) 。

所有这些方法的变体都是可能的。

可以将多台计算机链接在一起以利用多种传输方法。 您可以创建复杂的传输序列，以考虑技术人员的位置、符号所在的位置，以及是否有防火墙阻止连接在某些方向。 有关一些示例，请参阅 [高级远程调试方案](advanced-remote-debugging-scenarios.md) 。

甚至可以在一台计算机上执行远程调试。 例如，启动低特权进程服务器并使用高特权智能客户端连接到它可能会很有用。

 

 





