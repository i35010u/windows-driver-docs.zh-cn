---
title: 切换模式
description: 切换模式
ms.assetid: 167e5352-4ebc-423d-bf4f-ba1d459b394f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fffbf3388be79be5a88d0b5539e7550112598a98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335496"
---
# <a name="switching-modes"></a>切换模式


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


当您[控制用户模式下从内核调试程序调试](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)，您遇到了四种不同模式，并且可以通过多种方式在它们之间切换。

**请注意**  中描述此方案中，*应用程序的目标*正在调试的用户模式应用程序是指*目标计算机*指的计算机，包含目标应用程序和 CDB 或 NTSD 过程，并*主机计算机*指包含内核调试程序的计算机。

 

将遇到的以下四种模式：

<span id="User-mode_debugging"></span><span id="user-mode_debugging"></span><span id="USER-MODE_DEBUGGING"></span>*用户模式下调试*  
目标计算机和目标应用程序均已冻结。 在显示的用户模式下调试提示[调试器命令窗口](debugger-command-window.md)的内核调试程序。 在 WinDbg 中，在 WinDbg 窗口的下部的面板中的提示符将显示输入&gt;。 您可以输入在此提示符下，命令，如同它们输入的用户模式下在调试期间，以分析目标应用程序的状态或将导致其运行或单步执行它的执行。 符号文件、 扩展 Dll 和调试器访问其他文件将在目标计算机，而非主机计算机上的这些文件。

<span id="Target_application_execution"></span><span id="target_application_execution"></span><span id="TARGET_APPLICATION_EXECUTION"></span>*目标应用程序执行*  
目标计算机运行的，目标应用程序正在运行，并且正在等待调试程序。 此模式下是与允许在普通调试运行的目标相同。

<span id="Sleep_mode"></span><span id="sleep_mode"></span><span id="SLEEP_MODE"></span>*睡眠模式*  
目标计算机正在运行，但目标应用程序已被冻结，且这两个调试器已冻结。 如果您只需在目标计算机上的某些内容，但不是希望更改调试会话的状态，此模式非常有用。

<span id="Kernel-mode_debugging"></span><span id="kernel-mode_debugging"></span><span id="KERNEL-MODE_DEBUGGING"></span>*内核模式调试*  
目标计算机和目标应用程序均已冻结。 内核模式调试提示 kd&gt;内核调试程序在调试器命令窗口中显示。 此模式是典型的内核模式调试状态。

在用户模式下调试模式下开始会话。 下面的操作和事件会导致要更改的模式：

-   若要从用户模式下对目标应用程序执行调试切换，请使用[ **g （转向）** ](g--go-.md)命令在`Input>`提示符。

-   若要从用户模式下调试目标应用程序执行，并返回到用户模式下调试暂时切换，请使用步骤、 追踪或其他临时执行命令。 此类命令的列表，请参阅[控制目标](controlling-the-target.md)。

-   若要从用户模式下调试睡眠模式切换，请使用[ **.sleep （暂停调试器）** ](-sleep--pause-debugger-.md)命令。 此命令被超时。 当时间到期时，系统将恢复为用户模式下调试。

-   若要从用户模式下调试到内核模式调试切换，请使用[ **.breakin （中断添加到内核调试程序）** ](-breakin--break-to-the-kernel-debugger-.md)命令。 请注意， **.breakin**可能会因访问被拒绝错误，如果调用进程不具有管理员权限。 在这种情况下，通过发出一个短切换到 KD **.sleep**命令并按 CTRL + C。

-   可以从目标应用程序执行切换到用户模式下调试仅在某些环境中。 如果目标计算机正在运行 Microsoft Windows XP 或更高版本的 Windows 操作系统，则可以使用[ **！ bpid** ](-bpid.md)扩展命令。 如果使用 CDB (而不是 NTSD)，可以激活目标计算机上的 CDB 窗口，并按 CTRL + C。

-   如果目标应用程序命中断点，遇到的异常，遇到一些其他受控的事件或结束，从目标应用程序执行系统切换到用户模式下调试。 尤其是在您使用的 NTSD，应该提前计划此类事件。 有关这些事件的详细信息，请参阅[使用断点](using-breakpoints2.md)并[控制异常和事件](controlling-exceptions-and-events.md)。

-   若要从目标应用程序执行切换到内核模式调试，按 CTRL + C 在 KD 窗口中，按 CTRL + BREAK 或单击**中断**上**调试**WinDbg 窗口中，或者按 SYSRQ 或 ALT + SYSRQ 菜单在目标计算机键盘。 （如果内核调试程序是 KD 和内核调试程序用户模式下调试程序与之通信的同时按 CTRL + C，用户模式下调试程序可能会捕获您按 CTRL + C。）

-   如果调试器遇到了内核错误或者您使用 Breakin.exe 工具，系统从切换目标应用程序执行到内核模式调试。

-   若要从休眠模式切换到用户模式下调试，请等待休眠时间以到期时，使用目标计算机上启动一个新的 CDB 进程-唤醒[**命令行选项**](cdb-command-line-options.md)，或使用[ **.wake （唤醒调试器）** ](-wake--wake-debugger-.md)命令 CDB 或 NTSD 目标计算机上的不同副本。

-   若要切出内核模式调试，请使用[ **g （转向）** ](g--go-.md)命令在`kd>`提示符。 此命令返回到用户模式下调试或目标应用程序执行 （取两者是最近使用过的状态）。

 

 





