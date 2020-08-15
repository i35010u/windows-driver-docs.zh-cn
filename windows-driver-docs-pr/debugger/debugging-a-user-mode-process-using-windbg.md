---
title: 使用 WinDbg 调试用户模式进程
description: 您可以使用 WinDbg 附加到正在运行的进程或生成并附加到新进程。
ms.assetid: 65677DE4-4C91-4E24-B9BC-0924619C7307
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f9943dc9ee0ed0cbf271cca93d0a8efad62b858
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253099"
---
# <a name="span-iddebuggerdebugging_a_user-mode_process_using_windbgspandebugging-a-user-mode-process-using-windbg"></a><span id="debugger.debugging_a_user-mode_process_using_windbg"></span>使用 WinDbg 调试用户模式进程


您可以使用 WinDbg 附加到正在运行的进程或生成并附加到新进程。

## <a name="span-idattaching_to_a_running_processspanspan-idattaching_to_a_running_processspanspan-idattaching_to_a_running_processspanattaching-to-a-running-process"></a><span id="Attaching_to_a_Running_Process"></span><span id="attaching_to_a_running_process"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS"></span>附加到正在运行的进程


可以通过多种方式将 WinDbg 附加到正在运行的进程。 无论选择哪种方法，都需要进程 ID 或进程名称。 进程 ID 是由操作系统分配的数字。 有关如何确定进程 ID 和进程名称的详细信息，请参阅 [查找进程 id](finding-the-process-id.md)。

### <a name="span-idwindbg_menuspanspan-idwindbg_menuspanspan-idwindbg_menuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg 菜单

当 WinDbg 处于休眠模式时，您可以通过从 "**文件**" 菜单中选择 "**附加到进程**" 或按**F6**，附加到正在运行的进程。

在 " **附加到进程** " 对话框中，选择要调试的进程，然后选择 **"确定"**。

### <a name="span-idcommand_prompt1spanspan-idcommand_prompt1spancommand-prompt"></a><span id="command_prompt1"></span><span id="COMMAND_PROMPT1"></span>命令提示符

在命令提示符窗口中，您可以在启动 WinDbg 时附加到正在运行的进程。 使用以下命令之一：

-   **windbg-p** *ProcessID*
-   **windbg-pn** *ProcessName*

其中 *ProcessID* 是正在运行的进程的进程 ID，或 *ProcessName* 是正在运行的进程的名称。

有关命令行语法的详细信息，请参阅 [**WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-iddebugger_command_window1spanspan-iddebugger_command_window1spandebugger-command-window"></a><span id="debugger_command_window1"></span><span id="DEBUGGER_COMMAND_WINDOW1"></span>调试器命令窗口

如果 WinDbg 已经在调试一个或多个进程，则可以通过在[调试器命令窗口](the-debugger-command-window.md)中使用 " [** (附加到进程") **](-attach--attach-to-process-.md)命令附加到正在运行的进程。

调试器始终同时启动多个目标进程，除非它们的某些线程被冻结或挂起。

如果 [**attach**](-attach--attach-to-process-.md) 命令成功，则调试器将在下一次发出执行命令时附加到指定的进程。 如果在一行中多次使用此命令，则在使用此命令时，调试器需要执行多次。

## <a name="span-idattaching_to_a_running_process_noninvasivelyspanspan-idattaching_to_a_running_process_noninvasivelyspanspan-idattaching_to_a_running_process_noninvasivelyspanattaching-to-a-running-process-noninvasively"></a><span id="Attaching_to_a_Running_Process_Noninvasively"></span><span id="attaching_to_a_running_process_noninvasively"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_NONINVASIVELY"></span>附加到正在运行的进程 Noninvasively


如果希望调试正在运行的进程，并且仅影响其执行的最小操作，则应调试进程 [noninvasively](noninvasive-debugging--user-mode-.md)。

### <a name="span-idwindbg_menu1spanspan-idwindbg_menu1spanwindbg-menu"></a><span id="windbg_menu1"></span><span id="WINDBG_MENU1"></span>WinDbg 菜单

当 WinDbg 处于休眠模式时，您可以通过从 "**文件**" 菜单中选择 "**附加到进程**" 或按**F6**，noninvasively 调试正在运行的进程。

出现 " **附加到进程** " 对话框时，选中 " **Noninvasive** " 复选框。 然后，选择包含所需的进程 ID 和名称的行。  (您还可以在 " **进程 id** " 框中输入进程 id。 ) 最后，选择 **"确定"**。

### <a name="span-idcommand_prompt2spanspan-idcommand_prompt2spancommand-prompt"></a><span id="command_prompt2"></span><span id="COMMAND_PROMPT2"></span>命令提示符

在命令提示符窗口中，您可以在启动 WinDbg 时附加到正在运行的进程 noninvasively。 使用以下命令之一：

**windbg-pv-p** *ProcessID* 
 **windbg-pv-pn** *ProcessName*还有其他一些有用的命令行选项。 有关命令行语法的详细信息，请参阅 [**WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-iddebugger_command_window2spanspan-iddebugger_command_window2spandebugger-command-window"></a><span id="debugger_command_window2"></span><span id="DEBUGGER_COMMAND_WINDOW2"></span>调试器命令窗口

如果调试器已处于活动状态，则可以使用 noninvasively 调试正在运行的进程，方法是在[调试器命令窗口](the-debugger-command-window.md)中使用 " [** (附加到进程) **](-attach--attach-to-process-.md) " 命令。

如果调试器已在调试一个或多个进程 invasively，则可以使用 **. attach** 命令。 如果 WinDbg 处于休眠状态，则不能使用此命令。

如果 **attach-v** 命令成功，则调试器将在下一次发出执行命令时调试指定的进程。 由于在 noninvasive 调试期间不允许执行，因此调试器无法 noninvasively 一次调试多个进程。 此限制还意味着使用 **. attach** 命令可能会使现有的侵害性调试会话不太有用。

## <a name="span-idspawning_a_new_processspanspan-idspawning_a_new_processspanspan-idspawning_a_new_processspanspawning-a-new-process"></a><span id="Spawning_a_New_Process"></span><span id="spawning_a_new_process"></span><span id="SPAWNING_A_NEW_PROCESS"></span>生成新进程


WinDbg 可以启动用户模式应用程序，然后调试应用程序。 该应用程序按名称指定。 调试器还可以自动附加到子进程 (初始目标进程) 启动的其他进程。

调试器创建的进程 (也称为生成进程) 的行为与调试器不创建的进程略有不同。

调试器创建的进程使用特殊的调试堆，而不是使用标准堆 API。 您可以通过使用 " \_ 无 \_ 调试 \_ 堆 [环境变量](general-environment-variables.md) " 或 **-hd** 命令行选项，强制生成的进程使用标准堆而不是调试堆。

此外，由于目标应用程序是调试器的子进程，因此它将继承调试器的权限。 此权限可能会使目标应用程序执行某些无法执行的操作。 例如，目标应用程序可能会影响受保护的进程。

### <a name="span-idwindb_menu2spanspan-idwindb_menu2spanwindbg-menu"></a><span id="windb_menu2"></span><span id="WINDB_MENU2"></span>WinDbg 菜单

当 WinDbg 处于休眠模式时，您可以通过从 "文件" 菜单中选择 "**打开可执行****文件**" 或按 CTRL + E 来生成新的进程。

当 "打开可执行文件" 对话框出现时，请在 **"文件名" 框中** 输入可执行文件的完整路径，或使用 " **查找范围** " 列表选择所需的路径和文件名。

如果要在用户模式应用程序中使用任何命令行参数，请在 " **自变量** " 框中输入。 如果要从默认目录更改起始目录，请在 " **启动** 目录" 框中输入目录路径。 如果希望 WinDbg 附加到子进程，请选中 " **调试子进程** " 复选框。

做出选择后，选择 " **打开**"。

### <a name="span-idcommand_promptspanspan-idcommand_promptspanspan-idcommand_promptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>命令提示符

在命令提示符窗口中，您可以在启动 WinDbg 时生成新的进程。 使用以下命令：

**windbg \[ -o \] ** *ProgramName* **\[** <em>参数</em>**\]**

**-O**选项将使调试器附加到子进程。 还有其他一些有用的命令行选项。 有关命令行语法的详细信息，请参阅 [**WinDbg 命令行选项**](windbg-command-line-options.md)。

### <a name="span-iddebugger_command_window3spanspan-iddebugger_command_window3spandebugger-command-window"></a><span id="debugger_command_window3"></span><span id="DEBUGGER_COMMAND_WINDOW3"></span>调试器命令窗口

如果 WinDbg 已经在调试一个或多个进程，则可以使用创建新的进程，方法是在[调试器命令窗口](the-debugger-command-window.md)中创建[** (创建进程) **](-create--create-process-.md)命令。

调试器将始终同时启动多个目标进程，除非它们的某些线程被冻结或挂起。

如果 [**创建**](-create--create-process-.md) 命令成功，则调试器将在下一次发出执行命令时创建指定的进程。 如果在一行中多次使用此命令，则在使用此命令时，调试器需要执行多次。

你可以在[**创建**](-create--create-process-.md)之前，通过使用[**. createdir (Set Create create Process directory) **](-createdir--set-created-process-directory-.md)命令来控制应用程序的起始目录。 可以使用 **createdir-I** 命令或 **-noinh** 命令行选项来控制目标应用程序是否继承调试器的句柄。

您可以使用 [**. childdbg (调试子进程) **](-childdbg--debug-child-processes-.md) 命令来激活或停用子进程调试。

## <a name="span-idreattaching_to_a_processspanspan-idreattaching_to_a_processspanspan-idreattaching_to_a_processspanreattaching-to-a-process"></a><span id="Reattaching_to_a_Process"></span><span id="reattaching_to_a_process"></span><span id="REATTACHING_TO_A_PROCESS"></span>重新附加到进程


如果调试器停止响应或冻结，则可以将新的调试器附加到目标进程。 有关如何在这种情况下附加调试器的详细信息，请参阅重新 [附加到目标应用程序](reattaching-to-the-target-application.md)。

 

 





