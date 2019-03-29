---
title: 使目标计算机崩溃和重新启动目标计算机
description: 本主题介绍了崩溃和重新启动目标计算机
ms.assetid: 7480e572-05ca-40c6-aa91-b1ab35e4496b
keywords: 调试、 调试，控制目标，崩溃目标计算机，重启目标计算机重新启动，启动进程，在系统发生崩溃，错误检查
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c176e7ba0f1e27535df92ddbc041ab384878384a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561758"
---
# <a name="crashing-and-rebooting-the-target-computer"></a>使目标计算机崩溃和重新启动目标计算机


## <span id="ddk_crashing_and_rebooting_the_target_computer_dbg"></span><span id="DDK_CRASHING_AND_REBOOTING_THE_TARGET_COMPUTER_DBG"></span>


当你执行内核调试时，你可能会导致目标计算机停止响应 (即*崩溃*或*bug 检查*) 通过发出[ **.crash （强制系统崩溃）** ](-crash--force-system-crash-.md)命令。 此命令将立即导致目标计算机停止响应。 调试器将内核模式转储文件写入是否已启用故障转储。 (有关这些文件的详细信息，请参阅[创建内核模式转储文件](creating-a-kernel-mode-dump-file.md)。)

若要重新启动目标计算机，请使用[ **.reboot （重新启动目标计算机）** ](-reboot--reboot-target-computer-.md)命令。

如果你想要创建崩溃转储文件，然后重新启动目标计算机，则你应发出 **.crash**命令后, 跟 **.reboot**命令。 如果只想重新启动，请 **.crash**命令不是必需。

在启动过程的早期阶段，主计算机和目标计算机之间的连接将丢失。 有关目标计算机的任何信息不可供调试器。

连接已断开后，调试器将关闭所有符号文件，并卸载所有调试器扩展。 此时，所有断点都会丢失，如果都在运行 KD 或 CDB。 在 WinDbg 中，您可以保存当前工作区。 此操作将保存所有断点。

如果你想要在此时在调试会话结束，使用[ **CTRL + B** ](ctrl-b--quit-local-debugger-.md)命令 （在 KD)，或单击**退出**上**文件**菜单 （位于 WinDbg).

如果您不退出调试器，足够多的启动过程完成后，是重新建立连接。 符号和扩展会在此处重新加载。 如果运行 WinDbg，将重新加载内核模式下工作区。

可以让调试器在自动分解为目标计算机重新启动过程中在两个可能的时间：

-   如果第一个内核模块加载到内存

-   当内核初始化

若要设置自动断点的第一个内核模块加载时，使用 **-d** [命令行选项](command-line-options.md)。

运行调试器后，还可以更改中断状态：

-   控件的初始模块负载和内核初始化断点所有异常和事件都等。 这些事件出现，或忽略这些错误时，可以进入调试器。 您还可以自动执行这些断点被命中时指定的命令。 有关详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

-   使用[ **CTRL + K** ](ctrl-k--change-post-reboot-break-state-.md) KD 中的键盘快捷方式[CTRL + ALT + K](debug---kernel-connection---cycle-initial-break.md)键盘快捷方式中的 WinDbg 中，和调试 |内核连接 |周期初始中断命令在 WinDbg 中的更改中断状态。 使用这些命令，每次三个状态之间切换的调试器： 不自动中断内核初始化时中断，并在第一个内核模块加载中断。 此方法不能同时激活两个自动断点。

 

 





