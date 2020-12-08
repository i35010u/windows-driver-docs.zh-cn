---
title: 非侵入式调试（用户模式）
description: 非侵入式调试（用户模式）
keywords:
- 进程，调试 noninvasively
- noninvasive 调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb60ce2d725ae1b22935da010481325ca14026f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833655"
---
# <a name="noninvasive-debugging-user-mode"></a>非侵入式调试（用户模式）


## <span id="ddk_noninvasive_debugging_user_mode__dbg"></span><span id="DDK_NONINVASIVE_DEBUGGING_USER_MODE__DBG"></span>


如果用户模式应用程序已在运行，则调试器可以 *noninvasively* 调试。 使用 noninvasive 调试时，调试操作不会有多个。 但是，你可以最大程度地减少调试器与目标应用程序的干扰。 如果目标应用程序停止响应，Noninvasive 调试非常有用。

在 noninvasive 调试中，调试器实际上不会附加到目标应用程序。 调试器会挂起目标的所有线程，并有权访问目标的内存、寄存器和其他此类信息。 但是，调试器无法控制目标，因此，类似 [**g (中转)**](g--go-.md) 的命令不起作用。

如果尝试执行 noninvasive 调试期间不允许执行的命令，将收到一条错误消息，指出 "调试器未附加，因此无法监视进程执行"。

### <a name="span-idselecting_the_process_to_debugspanspan-idselecting_the_process_to_debugspanselecting-the-process-to-debug"></a><span id="selecting_the_process_to_debug"></span><span id="SELECTING_THE_PROCESS_TO_DEBUG"></span>选择要调试的进程

可以按进程 ID 指定目标应用程序 (PID) 或进程名称。

如果按名称指定应用程序，则应使用进程的完整名称，包括文件扩展名。 如果两个进程具有相同的名称，则必须改用进程 ID。

有关如何确定进程 ID 和进程名称的详细信息，请参阅 [查找进程 id](finding-the-process-id.md)。

有关启动和停止 noninvasive 调试会话的信息，请参阅以下主题：

-   [使用 WinDbg 调试用户模式进程](debugging-a-user-mode-process-using-windbg.md)
-   [使用 CDB 调试用户模式进程](debugging-a-user-mode-process-using-cdb.md)

### <a name="span-idcdb_command_linespanspan-idcdb_command_linespancdb-command-line"></a><span id="cdb_command_line"></span><span id="CDB_COMMAND_LINE"></span>CDB 命令行

若要 noninvasively 从 CDB 命令行调试正在运行的进程，请使用以下语法指定-pv 选项、-p 选项和进程 ID。

**cdb-pv-p** *ProcessID*

或者，若要通过指定进程名称 noninvasively 调试正在运行的进程，请改用以下语法。

**cdb-pv-pn** *ProcessName*

还有其他一些有用的命令行选项。 有关命令行语法的详细信息，请参阅 [**CDB Command-Line 选项**](cdb-command-line-options.md)。

### <a name="span-idwindbg_command_linespanspan-idwindbg_command_linespanwindbg-command-line"></a><span id="windbg_command_line"></span><span id="WINDBG_COMMAND_LINE"></span>WinDbg 命令行

若要 noninvasively 从 WinDbg 命令行调试正在运行的进程，请使用以下语法指定-pv 选项、-p 选项和进程 ID。

**windbg-pv-p** *ProcessID*

或者，若要通过指定进程名称 noninvasively 调试正在运行的进程，请改用以下语法。

**windbg-pv-pn** *ProcessName*

还有其他一些有用的命令行选项。 有关命令行语法的详细信息，请参阅 [**WinDbg Command-Line 选项**](windbg-command-line-options.md)。

### <a name="span-idwindbg_menuspanspan-idwindbg_menuspanwindbg-menu"></a><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg 菜单

当 WinDbg 处于休眠模式时，您可以通过在 "文件" 菜单上单击 "附加到进程" 或按 F6，noninvasively 调试正在运行的进程。

出现 "附加到进程" 对话框时，选中 "Noninvasive" 复选框。 然后，选择包含所需的进程 ID 和名称的行。  (您还可以在 "进程 ID" 框中输入进程 ID。 ) 最后，单击 "确定"。

### <a name="span-iddebugger_command_windowspanspan-iddebugger_command_windowspandebugger-command-window"></a><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口

如果调试器已处于活动状态，则可以使用 noninvasively 调试正在运行的进程，方法是在 [调试器命令窗口](the-debugger-command-window.md)中使用 " [**(附加到进程)**](-attach--attach-to-process-.md) " 命令。

如果调试器已在调试一个或多个进程 invasively，则可以使用. attach 命令。 如果它处于休眠状态，但未处于休眠的 WinDbg 中，则可以在 CDB 中使用此命令。

如果 attach-v 命令成功，则调试器将在下一次发出执行命令时调试指定的进程。 由于在 noninvasive 调试期间不允许执行，因此调试器无法 noninvasively 一次调试多个进程。 此限制还意味着使用. attach 命令可能会使现有的侵害性调试会话不太有用。

### <a name="span-idbeginning_the_debugging_sessionspanspan-idbeginning_the_debugging_sessionspanbeginning-the-debugging-session"></a><span id="beginning_the_debugging_session"></span><span id="BEGINNING_THE_DEBUGGING_SESSION"></span>开始调试会话

有关如何开始调试会话的详细信息，请参阅 [调试器操作](debugger-operation-win8.md)。

 

 





