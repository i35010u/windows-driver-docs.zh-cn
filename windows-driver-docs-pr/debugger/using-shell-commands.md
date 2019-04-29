---
title: 使用 Shell 命令
description: 使用 Shell 命令
ms.assetid: 16df2592-0e7d-4cd3-bc35-5323578cf555
keywords:
- shell 命令
- shell 命令概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 021c12590d078be1cf898afa1b62e475ecf7960d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353166"
---
# <a name="using-shell-commands"></a>使用 Shell 命令


## <span id="ddk_using_shell_commands_dbg"></span><span id="DDK_USING_SHELL_COMMANDS_DBG"></span>


调试器可以传输到 Microsoft Windows 环境在其中运行调试器的某些命令。

可以使用[ **.shell （命令行界面）** ](-shell--command-shell-.md)在任何 Windows 调试程序命令。 使用此命令，您可以直接从调试器中执行应用程序或 Microsoft MS-DOS 命令。 如果您正在执行[远程调试](remote-debugging.md)，在服务器上执行这些 shell 命令。

[ **.Noshell （禁止 Shell 命令）** ](-noshell--prohibit-shell-commands-.md)命令或 **-noshell** [命令行选项](command-line-options.md)禁用所有 shell 命令。 禁用了命令运行调试器时，即使在开始新的调试会话。 这些命令将保持禁用状态，即使您发出[ **.restart （重新启动内核连接）** ](-restart--restart-kernel-connection-.md) KD 命令。

如果正在调试的服务器，你可能想要禁用 shell 命令。 如果可用的 shell，可以使用远程连接 **.shell**命令以更改您的计算机。

### <a name="span-idnetworkdrivecontrolspanspan-idnetworkdrivecontrolspannetwork-drive-control"></a><span id="network_drive_control"></span><span id="NETWORK_DRIVE_CONTROL"></span>网络驱动器控制

在 WinDbg 中，可以使用[文件 |映射网络驱动器](file---map-network-drive.md)和[文件 |断开网络驱动器的连接](file---disconnect-network-drive.md)命令来控制网络驱动器映射。 始终在 WinDbg，永远不会在远程连接到 WinDbg 的任何计算机运行的计算机上进行这些更改。

 

 





