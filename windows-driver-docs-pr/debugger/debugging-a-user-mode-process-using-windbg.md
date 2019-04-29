---
title: 使用 WinDbg 调试用户模式进程
description: 可以使用 WinDbg 附加到正在运行的进程或重新生成并附加到新的进程。
ms.assetid: 65677DE4-4C91-4E24-B9BC-0924619C7307
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a01ee2d466725d3ec9000de00af43ab85bec12ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359064"
---
# <a name="span-iddebuggerdebuggingauser-modeprocessusingwindbgspandebugging-a-user-mode-process-using-windbg"></a><span id="debugger.debugging_a_user-mode_process_using_windbg"></span>调试使用 WinDbg 的用户模式进程


可以使用 WinDbg 附加到正在运行的进程或重新生成并附加到新的进程。

## <a name="span-idattachingtoarunningprocessspanspan-idattachingtoarunningprocessspanspan-idattachingtoarunningprocessspanattaching-to-a-running-process"></a><span id="Attaching_to_a_Running_Process"></span><span id="attaching_to_a_running_process"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS"></span>将附加到正在运行的进程


有几种方法可以使用 WinDbg 将附加到正在运行的进程。 无论您选择的方法，将需要的进程 ID 或进程名称。 进程 ID 是由操作系统分配的数字。 有关如何确定进程 ID 和进程名称的详细信息，请参阅[查找进程 ID](finding-the-process-id.md)。

### <a name="span-idwindbgmenuspanspan-idwindbgmenuspanspan-idwindbgmenuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg Menu

WinDbg 在处于休眠模式时，您可以通过选择附加到正在运行的进程**附加到进程**从**文件**菜单或通过按**F6**。

在中**附加到进程**对话框框中，选择你想要调试，并单击的进程**确定**。

### <a name="span-idcommandprompt1spanspan-idcommandprompt1spancommand-prompt"></a><span id="command_prompt1"></span><span id="COMMAND_PROMPT1"></span>命令提示符

在命令提示符窗口中，您可以将附加到正在运行的进程启动 WinDbg 时。 使用以下命令之一：

-   **windbg -p** *ProcessID*
-   **windbg -pn** *ProcessName*

其中*ProcessID*是正在运行的进程的进程 ID 或*ProcessName*是正在运行的进程的名称。

有关命令行语法的详细信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-iddebuggercommandwindow1spanspan-iddebuggercommandwindow1spandebugger-command-window"></a><span id="debugger_command_window1"></span><span id="DEBUGGER_COMMAND_WINDOW1"></span>调试器命令窗口

如果 WinDbg 已调试一个或多个进程，则可以通过使用附加到正在运行的进程[ **.attach （附加到进程）** ](-attach--attach-to-process-.md)命令[调试器命令窗口](the-debugger-command-window.md).

调试器始终启动多个目标进程同时，除非它们的线程的一些被冻结或挂起。

如果[ **.attach** ](-attach--attach-to-process-.md)命令成功，将调试器附加到指定的进程发出执行命令，在调试器下一次。 如果行中多次使用此命令，必须请求无数次，使用此命令在调试器的执行。

## <a name="span-idattachingtoarunningprocessnoninvasivelyspanspan-idattachingtoarunningprocessnoninvasivelyspanspan-idattachingtoarunningprocessnoninvasivelyspanattaching-to-a-running-process-noninvasively"></a><span id="Attaching_to_a_Running_Process_Noninvasively"></span><span id="attaching_to_a_running_process_noninvasively"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_NONINVASIVELY"></span>Noninvasively 附加到正在运行的进程


如果你想要调试正在运行的进程，仅在最低程度会影响在其执行中，应调试进程[noninvasively](noninvasive-debugging--user-mode-.md)。

### <a name="span-idwindbgmenu1spanspan-idwindbgmenu1spanwindbg-menu"></a><span id="windbg_menu1"></span><span id="WINDBG_MENU1"></span>WinDbg Menu

WinDbg 在处于休眠模式时，可以通过选择 noninvasively 调试正在运行的进程**附加到进程**从**文件**菜单或通过按**F6**。

当**附加到进程**对话框后，选择**Noninvasive**复选框。 然后，选择包含进程 ID 和所需名称的行。 (您还可以输入中的进程 ID**进程 ID**框。)最后，单击**确定**。

### <a name="span-idcommandprompt2spanspan-idcommandprompt2spancommand-prompt"></a><span id="command_prompt2"></span><span id="COMMAND_PROMPT2"></span>命令提示符

在命令提示符窗口中，您可以将附加到正在运行的进程 noninvasively 启动 WinDbg 时。 使用以下命令之一：

**windbg-pv-p** *ProcessID*
**windbg-pv pn** *ProcessName*有几个其他有用的命令行选项。 有关命令行语法的详细信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-iddebuggercommandwindow2spanspan-iddebuggercommandwindow2spandebugger-command-window"></a><span id="debugger_command_window2"></span><span id="DEBUGGER_COMMAND_WINDOW2"></span>调试器命令窗口

如果调试器已处于活动状态，可以通过使用 noninvasively 调试正在运行的进程[ **.attach-v （附加到进程）** ](-attach--attach-to-process-.md)命令，在[调试器命令窗口](the-debugger-command-window.md)。

可以使用 **.attach**命令如果调试程序已调试一个或多个进程 invasively。 如果 WinDbg 处于休眠状态，则无法使用此命令。

如果 **.attach v**命令成功，调试器将调试指定的进程发出执行命令，在调试器下一次。 在非侵入调试过程中不允许执行，因为调试器不能 noninvasively 调试一次的多个进程。 此限制也意味着，使用 **.attach v**命令可能会使现有的侵入性调试会话不太有用。

## <a name="span-idspawninganewprocessspanspan-idspawninganewprocessspanspan-idspawninganewprocessspanspawning-a-new-process"></a><span id="Spawning_a_New_Process"></span><span id="spawning_a_new_process"></span><span id="SPAWNING_A_NEW_PROCESS"></span>生成新的进程


WinDbg 可以启动在用户模式应用程序和调试应用程序。 按名称指定应用程序。 可以还会自动将调试器附加到子进程 （原始目标进程启动的其他进程） 中。

调试器创建 （也称为生成的进程） 的进程的行为略有不同的调试器不会创建进程。

而不是使用标准堆 API，调试器创建的进程使用特殊的调试堆。 你可以强制执行生成的进程，而不是调试堆中通过使用标准堆\_否\_调试\_堆[环境变量](general-environment-variables.md)或 **-hd**命令行选项。

此外，由于目标应用程序是在调试器的子进程，它将继承的调试程序的权限。 此权限可能会使目标应用程序来执行其否则无法执行某些操作。 例如，目标应用程序可能能够影响受保护的进程。

### <a name="span-idwindbmenu2spanspan-idwindbmenu2spanwindbg-menu"></a><span id="windb_menu2"></span><span id="WINDB_MENU2"></span>WinDbg Menu

WinDbg 在处于休眠模式时，可以通过选择生成一个新的进程**打开可执行文件**从**文件**菜单或通过按 CTRL + E。

可执行文件打开对话框出现时，输入中的可执行文件的完整路径**文件名**框中，或使用**查找**列表以选择所需的路径和文件名。

如果你想要用户模式应用程序中使用任何命令行参数，则输入它们中**自变量**框。 如果你想要更改的开始目录从默认目录，请输入中的目录路径**启动**目录。 如果你想要附加到子进程的 WinDbg，请选择**调试子进程也**复选框。

进行选择后，单击**打开**。

### <a name="span-idcommandpromptspanspan-idcommandpromptspanspan-idcommandpromptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>命令提示符

在命令提示符窗口中，可以生成一个新进程，启动 WinDbg 时。 使用以下命令：

**windbg \[-o\]** *ProgramName* **\[**<em>Arguments</em>**\]**

**-O**选项将使调试器附加到子进程。 有几个其他有用的命令行选项。 有关命令行语法的详细信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-iddebuggercommandwindow3spanspan-iddebuggercommandwindow3spandebugger-command-window"></a><span id="debugger_command_window3"></span><span id="DEBUGGER_COMMAND_WINDOW3"></span>调试器命令窗口

如果 WinDbg 已调试一个或多个进程，您可以使用创建新的进程[ **.create （创建进程）** ](-create--create-process-.md)命令，在[调试器命令窗口](the-debugger-command-window.md)。

除非一些其线程被冻结或挂起调试器始终将同时启动多个目标进程。

如果[ **.create** ](-create--create-process-.md)命令成功，调试器将会发出执行命令时，调试器都会创建指定的进程。 如果行中多次使用此命令，必须请求无数次，使用此命令在调试器的执行。

你可以通过使用控制应用程序的开始目录[ **.createdir （设置创建的进程目录）** ](-createdir--set-created-process-directory-.md)命令之前[ **.create** ](-create--create-process-.md). 可以使用 **.createdir-我**命令或 **-noinh**命令行选项来控制目标应用程序是否继承调试器的句柄。

可以激活或停用使用调试子进程[ **.childdbg （调试子进程）** ](-childdbg--debug-child-processes-.md)命令。

## <a name="span-idreattachingtoaprocessspanspan-idreattachingtoaprocessspanspan-idreattachingtoaprocessspanreattaching-to-a-process"></a><span id="Reattaching_to_a_Process"></span><span id="reattaching_to_a_process"></span><span id="REATTACHING_TO_A_PROCESS"></span>重新附加到进程


如果在调试器停止响应或会冻结，您可以将新的调试器附加到目标进程。 有关如何附加调试器在这种情况的详细信息，请参阅[重新附加到目标应用程序](reattaching-to-the-target-application.md)。

 

 





