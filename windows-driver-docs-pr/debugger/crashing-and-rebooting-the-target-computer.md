---
title: 使目标计算机崩溃和重新启动目标计算机
description: 本主题介绍崩溃并重新启动目标计算机
keywords: 调试，调试，控制目标，崩溃目标计算机，重启目标计算机，重新启动，启动进程，系统崩溃，bug 检查
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21277eaffb0ed1d84a4a24879e3ac070238a6fa6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836883"
---
# <a name="crashing-and-rebooting-the-target-computer"></a>使目标计算机崩溃和重新启动目标计算机


## <span id="ddk_crashing_and_rebooting_the_target_computer_dbg"></span><span id="DDK_CRASHING_AND_REBOOTING_THE_TARGET_COMPUTER_DBG"></span>


执行内核调试时，可以通过发出 [**. 崩溃 (强制系统崩溃)**](-crash--force-system-crash-.md)命令，使目标计算机停止响应 (即 *崩溃* 或 *bug 检查*) 。 此命令会立即导致目标计算机停止响应。 如果已启用故障转储，则调试器会写入内核模式转储文件。  (有关这些文件的详细信息，请参阅 [创建 Kernel-Mode 转储文件](creating-a-kernel-mode-dump-file.md)。 ) 

若要重新启动目标计算机，请使用 " [**重启" (重新启动目标计算机)**](-reboot--reboot-target-computer-.md) 命令。

如果希望目标计算机创建故障转储文件，然后重新启动，则应发出 " **崩溃** " 命令，后 **跟 "restart** " 命令。 如果只需要重新启动，则不需要 **崩溃** 命令。

在启动过程的早期阶段，主计算机与目标计算机之间的连接将丢失。 没有关于目标计算机的信息可供调试器使用。

连接中断后，调试器将关闭所有符号文件并卸载所有调试器扩展。 此时，如果运行的是 KD 或 CDB，所有断点都将丢失。 在 WinDbg 中，可以保存当前工作区。 此操作保存所有断点。

如果要在此时结束调试会话，请在 KD 中使用 [**CTRL + B**](ctrl-b--quit-local-debugger-.md)命令 () 或单击 WinDbg)  (的 "**文件**" 菜单上的 "**退出**"。

如果不退出调试程序，则在启动过程完成后，将重新建立连接。 此时会重新加载符号和扩展。 如果正在运行 WinDbg，则会重新加载内核模式工作区。

可以告诉调试器在两次重新启动过程中自动中断目标计算机：

-   第一个内核模块加载到内存中时

-   内核初始化时

若要在第一个内核模块加载时设置自动断点，请使用 **-d** [命令行选项](command-line-options.md)。

还可以在调试器运行后更改中断状态：

-   控制初始模块加载和内核初始化断点，如所有异常和事件。 在发生这些事件时，可以中断调试器，或将其忽略。 你还可以在命中这些断点时，自动执行指定的命令。 有关详细信息，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。

-   使用 KD 中的 [**ctrl + K**](ctrl-k--change-post-reboot-break-state-.md) 快捷键、WinDbg 中的 [ctrl + ALT + K](debug---kernel-connection---cycle-initial-break.md) 快捷键和 Debug |内核连接 |在 WinDbg 中循环初始 Break 命令以更改中断状态。 每次使用这些命令时，调试器都会在三种状态之间切换：无自动中断、内核初始化中断以及第一次内核模块加载时中断。 此方法无法同时激活这两个自动断点。

 

 





