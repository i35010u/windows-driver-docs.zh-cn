---
title: 选择最佳的远程调试方法
description: 选择最佳的远程调试方法
ms.assetid: af048b78-cb80-44d2-854f-11e0991e3353
keywords:
- 远程调试，选择最佳方法
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 196f5f1348605b626266fbd5d0282d56f93e09a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375104"
---
# <a name="choosing-the-best-remote-debugging-method"></a>选择最佳的远程调试方法


## <span id="ddk_choosing_the_best_remote_debugging_method_dbg"></span><span id="DDK_CHOOSING_THE_BEST_REMOTE_DEBUGGING_METHOD_DBG"></span>


有两种主要方法执行远程调试，以及其他几种方法和大量的组合方法。

下面是一些提示可帮助您选择的最佳方法。

-   [通过在调试器的远程调试](remote-debugging-through-the-debugger.md)通常是最好的方法。 如果您只需有一台服务器和一个客户端并且可以自由地连接到对方，同一个调试程序二进制文件安装在客户端和服务器，并且的调试技术人员将操作客户端将能够与使用房间内有人服务器上，这是建议的方法。

    客户端和服务器可以运行任何版本的 Windows。 它们不需要为每个其他运行相同版本。

    如果客户端不能将连接请求发送到服务器，但服务器是否能够将请求发送到客户端，则可以使用的调试器中通过远程调试*反向连接*通过使用**clicon**参数。

-   [远程调试通过 remote.exe](remote-debugging-through-remote-exe.md)用于远程控制命令提示符窗口。 它可以用于远程控制 KD、 CDB 或 NTSD。 它不能用于 WinDbg。

    如果您的客户端不具有调试程序二进制文件的副本，必须使用 remote.exe 方法。

-   **进程服务器**或**KD 连接服务器**如果调试技术人员将无法再与与服务器房间内有人可以使用。 所有实际的调试工作完成由客户端 (称为*智能客户端*); 这将删除服务器本身上已存在第二个人员的需求。

    进程服务器用于用户模式下调试;KD 连接服务器用于内核模式调试。 非这一区别，它们的行为方式类似。

    此方法也是很有用，如果将运行服务器的计算机不能处理大量进程加载，或者如果技术人员运行客户端有权访问符号文件或源文件的机密并且不能为服务器访问。 但是，此方法不是将为快速或作为通过调试器的远程调试效率高。 此方法不能用于调试转储文件。

    请参阅[的进程服务器 （用户模式）](process-servers--user-mode-.md)并[KD 连接服务器 （内核模式）](kd-connection-servers--kernel-mode-.md)有关详细信息。

-   **Repeater**是中继两台计算机之间的数据的轻型代理服务器。 如果您正在执行通过调试器的远程调试，或者如果正在使用进程服务器，可以添加客户端和服务器之间 repeater。

    如果您的客户端和服务器不能直接相互通信，但每个可以访问外部计算机可能需要使用 repeater。 与重复字符也可以使用反向连接。 甚至可以使用两个重复字符某行中，但这很少需要。

    请参阅[重复字符](repeaters.md)有关详细信息。

-   还有可能从内核调试器控制 CDB （或 NTSD）。 这是尚未进行远程调试的另一种形式。 请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。

可能会出现在所有这些方法的变体。

则可以链接在一起以充分利用多个传输方法的多台计算机。 可以创建复杂的传输序列，考虑到技术人员所在，其中符号的位置，以及是否有防火墙阻止在特定方向上的连接。 请参阅[高级远程调试方案](advanced-remote-debugging-scenarios.md)有关一些示例。

甚至可以执行在一台计算机上进行远程调试。 例如，可能会很有用，若要启动低权限进程服务器，然后使用高特权的智能客户端连接到它。

 

 





