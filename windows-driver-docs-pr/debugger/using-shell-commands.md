---
title: 使用 Shell 命令
description: 使用 Shell 命令
keywords:
- shell 命令
- shell 命令，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6bb452a95493c9c4338b105601f74501a1a1b09
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803069"
---
# <a name="using-shell-commands"></a>使用 Shell 命令


## <span id="ddk_using_shell_commands_dbg"></span><span id="DDK_USING_SHELL_COMMANDS_DBG"></span>


调试器可以将某些命令传输到运行调试器的 Microsoft Windows 环境中。

可以在任何 Windows 调试器中使用 [**(命令行界面)**](-shell--command-shell-.md) 命令。 使用此命令，可以直接从调试器执行应用程序或 Microsoft MS-DOS 命令。 如果要执行 [远程调试](remote-debugging.md)，将在服务器上执行这些 shell 命令。

[**Noshell (禁止 Shell 命令)**](-noshell--prohibit-shell-commands-.md)命令或 **-noshell** [命令行选项](command-line-options.md)禁用所有 Shell 命令。 即使您开始新的调试会话，也会在调试器运行时禁用这些命令。 即使你发出了，命令仍会保持禁用状态 [**。重新启动 (在 KD 中重新启动内核连接)**](-restart--restart-kernel-connection-.md) 命令。

如果运行的是调试服务器，则可能需要禁用 shell 命令。 如果 shell 可用，则远程连接可以使用 **shell** 命令来更改计算机。

### <a name="span-idnetwork_drive_controlspanspan-idnetwork_drive_controlspannetwork-drive-control"></a><span id="network_drive_control"></span><span id="NETWORK_DRIVE_CONTROL"></span>网络驱动器控制

在 WinDbg 中，可以使用 [文件 |映射网络驱动器](file---map-network-drive.md) 和 [文件 |断开网络驱动器](file---disconnect-network-drive.md) 命令以控制网络驱动器映射。 这些更改始终发生在运行 WinDbg 的计算机上，而不是在远程连接到 WinDbg 的任何计算机上。

 

 





