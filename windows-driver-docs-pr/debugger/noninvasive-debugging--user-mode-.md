---
title: 非侵入调试 （用户模式）
description: 非侵入调试 （用户模式）
ms.assetid: 91f09fb1-9f5e-4081-89b3-78c95eada817
keywords:
- noninvasively 调试的进程
- 非侵入调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7474dabd0cbf06f71ab7ca976aa848e4eef21a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554548"
---
# <a name="noninvasive-debugging-user-mode"></a>非侵入调试 （用户模式）


## <span id="ddk_noninvasive_debugging_user_mode__dbg"></span><span id="DDK_NONINVASIVE_DEBUGGING_USER_MODE__DBG"></span>


如果在用户模式应用程序已在运行，调试器可以调试*noninvasively*。 非侵入调试后，您不具有尽可能多的调试操作。 但是，可以尽量减少与目标应用程序的调试程序的干扰。 非侵入调试是目标应用程序已停止响应的情况下很有用。

在非侵入调试中，调试器不会不实际附加到目标应用程序。 调试器挂起所有目标的线程，并有权访问目标的内存、 寄存器以及其他此类信息。 但是，调试器不能控制目标，以便命令，如[ **g （转向）** ](g--go-.md)不起作用。

如果您尝试执行非侵入调试过程中不允许使用的命令，你将收到错误消息，指出"未附加调试器，因此不能监视过程的执行。"

### <a name="span-idselectingtheprocesstodebugspanspan-idselectingtheprocesstodebugspanselecting-the-process-to-debug"></a><span id="selecting_the_process_to_debug"></span><span id="SELECTING_THE_PROCESS_TO_DEBUG"></span>选择要调试的进程

您可以指定由进程 ID (PID) 的目标应用程序或进程名称。

如果按名称指定的应用程序，应使用此过程中，其中包括文件扩展名的完整名称。 如果两个进程具有相同的名称，必须改为使用进程 ID。

有关如何确定进程 ID 和进程名称的详细信息，请参阅[查找进程 ID](finding-the-process-id.md)。

有关启动和停止非侵入的调试会话的信息，请参阅以下主题：

-   [调试使用 Visual Studio 的用户模式进程](debugging-a-user-mode-process-using-visual-studio.md)
-   [调试使用 WinDbg 的用户模式进程](debugging-a-user-mode-process-using-windbg.md)
-   [调试使用 CDB 的用户模式进程](debugging-a-user-mode-process-using-cdb.md)

### <a name="span-idcdbcommandlinespanspan-idcdbcommandlinespancdb-command-line"></a><span id="cdb_command_line"></span><span id="CDB_COMMAND_LINE"></span>CDB 命令行

若要 noninvasively 调试 CDB 命令行从正在运行的进程，请指定-pv 选项、-p 选项和进程 ID，在下面的语法。

**cdb -pv -p** *ProcessID*

或者，若要通过指定进程名称 noninvasively 调试正在运行的进程，请改为使用以下语法。

**cdb -pv -pn** *ProcessName*

有几个其他有用的命令行选项。 有关命令行语法的详细信息，请参阅[ **CDB 命令行选项**](cdb-command-line-options.md)。

### <a name="span-idwindbgcommandlinespanspan-idwindbgcommandlinespanwindbg-command-line"></a><span id="windbg_command_line"></span><span id="WINDBG_COMMAND_LINE"></span>WinDbg 命令行

若要 noninvasively 调试 WinDbg 命令行从正在运行的进程，请指定-pv 选项、-p 选项和进程 ID，在下面的语法。

**windbg -pv -p** *ProcessID*

或者，若要通过指定进程名称 noninvasively 调试正在运行的进程，请改为使用以下语法。

**windbg -pv -pn** *ProcessName*

有几个其他有用的命令行选项。 有关命令行语法的详细信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-idwindbgmenuspanspan-idwindbgmenuspanwindbg-menu"></a><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg Menu

WinDbg 在处于休眠模式时，您可以通过单击附加到进程文件菜单或通过按 F6 noninvasively 调试正在运行的进程。

附加到进程对话框出现时，选择非侵入的复选框。 然后，选择包含进程 ID 和所需名称的行。 （您还可以输入的进程 ID 的进程 ID 框中。）最后，单击确定。

### <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口

如果调试器已处于活动状态，可以通过使用 noninvasively 调试正在运行的进程[ **.attach-v （附加到进程）** ](-attach--attach-to-process-.md)命令，在[调试器命令窗口](the-debugger-command-window.md)。

如果调试器已 invasively 调试的一个或多个进程，可以使用.attach 命令。 在 CDB 如果处于休眠状态，但不是在处于休眠状态的 WinDbg 中，可以使用此命令。

如果.attach-v 命令成功，调试器将调试指定的进程发出执行命令，在调试器下一次。 在非侵入调试过程中不允许执行，因为调试器不能 noninvasively 调试一次的多个进程。 此限制也意味着，使用.attach-v 命令可能会使现有的侵入性调试会话不太有用。

### <a name="span-idbeginningthedebuggingsessionspanspan-idbeginningthedebuggingsessionspanbeginning-the-debugging-session"></a><span id="beginning_the_debugging_session"></span><span id="BEGINNING_THE_DEBUGGING_SESSION"></span>开始调试会话

有关如何开始调试会话的详细信息，请参阅[调试器操作](debugger-operation-win8.md)。

 

 





