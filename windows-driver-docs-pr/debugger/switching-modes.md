---
title: 切换模式
description: 切换模式
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f95a89177361bd420371d6178d39132d4cd24fc9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834685"
---
# <a name="switching-modes"></a>切换模式


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


当你 [从内核调试器控制用户模式调试](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)时，你将遇到四种不同模式，并且可以通过多种方式在它们之间进行切换。

**注意**   在描述此方案时， *目标应用程序* 是指正在调试的用户模式应用程序， *目标计算机* 指的是包含目标应用程序的计算机和 CDB 或 NTSD 进程， *主机计算机* 指的是包含内核调试器的计算机。

 

将遇到以下四种模式：

<span id="User-mode_debugging"></span><span id="user-mode_debugging"></span><span id="USER-MODE_DEBUGGING"></span>*用户模式调试*  
目标计算机和目标应用程序已冻结。 用户模式调试提示出现在内核调试器 [命令窗口的调试器](debugger-command-window.md) 中。 在 WinDbg 中，WinDbg 窗口的下部面板中的提示显示输入 &gt; 。 你可以在此提示符下输入命令，就像在用户模式调试过程中输入命令一样，可以分析目标应用程序的状态，或使其运行或单步执行执行。 符号文件、扩展 Dll 和调试器访问的其他文件将是目标计算机上的文件，而不是主计算机上的文件。

<span id="Target_application_execution"></span><span id="target_application_execution"></span><span id="TARGET_APPLICATION_EXECUTION"></span>*目标应用程序执行*  
目标计算机正在运行，目标应用程序正在运行，并且调试器正在等待。 此模式与在普通调试中运行目标相同。

<span id="Sleep_mode"></span><span id="sleep_mode"></span><span id="SLEEP_MODE"></span>*睡眠模式*  
目标计算机正在运行，但目标应用程序已冻结，并且两个调试器都已冻结。 如果你必须在目标计算机上执行某些操作，但又不想更改调试会话的状态，则此模式很有用。

<span id="Kernel-mode_debugging"></span><span id="kernel-mode_debugging"></span><span id="KERNEL-MODE_DEBUGGING"></span>*内核模式调试*  
目标计算机和目标应用程序已冻结。 内核模式调试提示 kd &gt; 出现在内核调试器命令窗口的调试器中。 此模式是典型的内核模式调试状态。

会话在用户模式调试模式下启动。 以下操作和事件将导致模式发生更改：

-   若要从用户模式调试切换到目标应用程序执行，请在提示符下使用 [**g (中转)**](g--go-.md) 命令 `Input>` 。

-   若要暂时从用户模式调试切换到目标应用程序执行，然后返回到用户模式调试，请使用步骤、跟踪或其他临时执行命令。 有关此类命令的列表，请参阅 [控制目标](controlling-the-target.md)。

-   若要从用户模式调试切换到睡眠模式，请使用 " [**睡眠 (暂停调试器")**](-sleep--pause-debugger-.md) 命令。 此命令已计时。 当时间到期时，系统将返回到用户模式调试。

-   若要从用户模式调试切换到内核模式调试，请使用 [**breakin (进入内核调试器)**](-breakin--break-to-the-kernel-debugger-.md) 命令。 请注意，如果调用进程没有管理员权限， **breakin** 可能会失败并出现 "拒绝访问" 错误。 在这种情况下，通过发出一个 short 的 **sleep** 命令并按 CTRL + C 切换到 KD。

-   只能在某些环境中从目标应用程序执行切换到用户模式调试。 如果目标计算机运行的是 Microsoft Windows XP 或更高版本的 Windows 操作系统，则可以使用 [**！ bpid**](-bpid.md) extension 命令。 如果使用的是 CDB (不是 NTSD) ，可以在目标计算机上激活 CDB 窗口，并按 CTRL + C。

-   如果目标应用程序点击了一个断点，遇到异常，遇到一些其他受控事件，或结束，则系统会从目标应用程序执行切换到用户模式调试。 应该提前规划此类事件，特别是在使用 NTSD 时。 有关这些事件的详细信息，请参阅 [使用断点](using-breakpoints2.md) 和 [控制异常和事件](controlling-exceptions-and-events.md)。

-   若要从目标应用程序执行切换到内核模式调试，请在 "KD" 窗口中按 CTRL + C，按 CTRL + BREAK，或者单击 "WinDbg" 窗口中 "**调试**" 菜单上的 "**中断**"，或在目标计算机键盘上按 SYSRQ 或 ALT + SYSRQ。  (如果内核调试程序是 KD 的，并且在内核调试器与用户模式调试器通信的同时按下 CTRL + C，则用户模式调试器可能会捕获按下 CTRL + C ) 

-   如果调试器遇到内核错误或使用 Breakin.exe 工具，则系统会从目标应用程序执行切换到内核模式调试。

-   若要从睡眠模式切换到用户模式调试，请等待睡眠时间过期，通过使用-唤醒 [**命令行选项**](cdb-command-line-options.md)在目标计算机上启动新的 CDB 进程，或在目标计算机上的 CDB 或 NTSD 的不同副本中使用 " [**(唤醒) 调试器**](-wake--wake-debugger-.md) " 命令。

-   若要切换出内核模式调试，请在提示符下使用 [**g (中转)**](g--go-.md) 命令 `kd>` 。 此命令返回到用户模式调试或目标应用程序执行 (这两种情况都是最近使用的状态) 。

 

 





