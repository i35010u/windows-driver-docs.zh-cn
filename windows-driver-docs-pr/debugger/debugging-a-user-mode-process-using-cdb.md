---
title: 使用 CDB 调试用户模式进程
description: 可以使用 CDB 附加到正在运行的进程，或生成并附加到新进程。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b16ba9c4bf6cc734488d60c65af485b63427fdd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841051"
---
# <a name="span-iddebuggerdebugging_a_user-mode_process_using_cdbspandebugging-a-user-mode-process-using-cdb"></a><span id="debugger.debugging_a_user-mode_process_using_cdb"></span>使用 CDB 调试用户模式进程


可以使用 CDB 附加到正在运行的进程，或生成并附加到新进程。

## <a name="span-idattaching_to_a_running_processspanspan-idattaching_to_a_running_processspanspan-idattaching_to_a_running_processspanattaching-to-a-running-process"></a><span id="Attaching_to_a_Running_Process"></span><span id="attaching_to_a_running_process"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS"></span>附加到正在运行的进程


### <a name="span-idcommand_prompt1spanspan-idcommand_prompt1spancommand-prompt"></a><span id="command_prompt1"></span><span id="COMMAND_PROMPT1"></span>命令提示符

在命令提示符窗口中，您可以在启动 CDB 时附加到正在运行的进程。 使用以下命令之一：

-   **cdb-p** *ProcessID*
-   **cdb-pn** *ProcessName*

其中 *ProcessID* 是正在运行的进程的进程 ID，或 *ProcessName* 是正在运行的进程的名称。

有关命令行语法的详细信息，请参阅 [**CDB Command-Line 选项**](cdb-command-line-options.md)。

### <a name="span-idcdb_command_window1spanspan-idcdb_command_window1spancdb-command-window"></a><span id="cdb_command_window1"></span><span id="CDB_COMMAND_WINDOW1"></span>CDB 命令窗口

如果调试器已在调试一个或多个进程，则可以使用 [**. attach (附加到进程)**](-attach--attach-to-process-.md) 命令附加到正在运行的进程。

调试器始终同时启动多个目标进程，除非它们的某些线程被冻结或挂起。

如果 [**attach**](-attach--attach-to-process-.md) 命令成功，则调试器将在下一次发出执行命令时附加到指定的进程。 如果在一行中多次使用此命令，则在使用此命令时，调试器需要执行多次。

## <a name="span-idattaching_to_a_running_process_noninvasivelyspanspan-idattaching_to_a_running_process_noninvasivelyspanspan-idattaching_to_a_running_process_noninvasivelyspanattaching-to-a-running-process-noninvasively"></a><span id="Attaching_to_a_Running_Process_Noninvasively"></span><span id="attaching_to_a_running_process_noninvasively"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_NONINVASIVELY"></span>附加到正在运行的进程 Noninvasively


如果希望调试正在运行的进程，并且仅影响其执行的最小操作，则应调试进程 [noninvasively](noninvasive-debugging--user-mode-.md)。

### <a name="span-idcommand_prompt2spanspan-idcommand_prompt2spancommand-prompt"></a><span id="command_prompt2"></span><span id="COMMAND_PROMPT2"></span>命令提示符

若要 noninvasively 从 CDB 命令行调试正在运行的进程，请使用以下语法指定 **-pv** 选项、 **-p** 选项和进程 ID。

**cdb-pv-p** *ProcessID*

或者，若要通过指定进程名称 noninvasively 调试正在运行的进程，请改用以下语法。

**cdb-pv-pn** *ProcessName*

还有其他一些有用的命令行选项。 有关命令行语法的详细信息，请参阅 [**CDB Command-Line 选项**](cdb-command-line-options.md)。

### <a name="span-idcdb_command_window2spanspan-idcdb_command_window2spancdb-command-window"></a><span id="cdb_command_window2"></span><span id="CDB_COMMAND_WINDOW2"></span>CDB 命令窗口

如果调试程序已处于活动状态，则可以通过输入 [**(附加到进程)**](-attach--attach-to-process-.md) 命令来 noninvasively 调试正在运行的进程。

如果调试器已在调试一个或多个进程 invasively，则可以使用 **. attach** 命令。

如果 **attach-v** 命令成功，则调试器将在下一次发出执行命令时调试指定的进程。 由于在 noninvasive 调试期间不允许执行，因此调试器无法 noninvasively 一次调试多个进程。 此限制还意味着使用 **. attach** 命令可能会使现有的侵害性调试会话不太有用。

## <a name="span-idspawning_a_new_processspanspan-idspawning_a_new_processspanspan-idspawning_a_new_processspanspawning-a-new-process"></a><span id="Spawning_a_New_Process"></span><span id="spawning_a_new_process"></span><span id="SPAWNING_A_NEW_PROCESS"></span>生成新进程


CDB 可以启动用户模式应用程序，然后调试应用程序。 该应用程序按名称指定。 调试器还可以自动附加到子进程 (初始目标进程) 启动的其他进程。

调试器创建的进程 (也称为生成进程) 的行为与调试器不创建的进程略有不同。

调试器创建的进程使用特殊的调试堆，而不是使用标准堆 API。 您可以通过使用 " \_ 无 \_ 调试 \_ 堆 [环境变量](general-environment-variables.md) " 或 **-hd** 命令行选项，强制生成的进程使用标准堆而不是调试堆。

此外，由于目标应用程序是调试器的子进程，因此它将继承调试器的权限。 此权限可能会使目标应用程序执行某些无法执行的操作。 例如，目标应用程序可能会影响受保护的进程。

在命令提示符窗口中，您可以在启动 CDB 时生成新的进程。 输入以下命令。

**cdb \[ -o \]** *ProgramName* **\[** <em>参数</em>**\]**

**-O** 选项将使调试器附加到子进程。 还有其他一些有用的命令行选项。 有关命令行语法的详细信息，请参阅 [**CDB Command-Line 选项**](cdb-command-line-options.md)。

如果调试器已在调试一个或多个进程，则可以通过输入 " [**创建 (创建进程)**](-create--create-process-.md) " 命令来创建新的进程。

调试器将始终同时启动多个目标进程，除非它们的某些线程被冻结或挂起。

如果 [**创建**](-create--create-process-.md) 命令成功，则调试器将在下一次发出执行命令时创建指定的进程。 如果在一行中多次使用此命令，则在使用此命令时，调试器需要执行多次。

你可以在 [**创建**](-create--create-process-.md)之前，通过使用 [**. createdir (Set Create create Process directory)**](-createdir--set-created-process-directory-.md)命令来控制应用程序的起始目录。 可以使用 **createdir-I** 命令或 **-noinh** 命令行选项来控制目标应用程序是否继承调试器的句柄。

您可以使用 [**. childdbg (调试子进程)**](-childdbg--debug-child-processes-.md) 命令来激活或停用子进程调试。

## <a name="span-idreattaching_to_a_processspanspan-idreattaching_to_a_processspanspan-idreattaching_to_a_processspanreattaching-to-a-process"></a><span id="Reattaching_to_a_Process"></span><span id="reattaching_to_a_process"></span><span id="REATTACHING_TO_A_PROCESS"></span>重新附加到进程


如果调试器停止响应或冻结，则可以将新的调试器附加到目标进程。 有关如何在这种情况下附加调试器的详细信息，请参阅重新 [附加到目标应用程序](reattaching-to-the-target-application.md)。

 

 





