---
title: 使用 CDB 调试用户模式进程
description: 可以使用 CDB 将附加到正在运行的进程或重新生成并附加到新进程。
ms.assetid: 0C56F6B5-0FBC-45C9-8AB7-218C00F90521
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb91baee79002457419a060312d1dd06b1136db2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324565"
---
# <a name="span-iddebuggerdebuggingauser-modeprocessusingcdbspandebugging-a-user-mode-process-using-cdb"></a><span id="debugger.debugging_a_user-mode_process_using_cdb"></span>调试使用 CDB 的用户模式进程


可以使用 CDB 将附加到正在运行的进程或重新生成并附加到新进程。

## <a name="span-idattachingtoarunningprocessspanspan-idattachingtoarunningprocessspanspan-idattachingtoarunningprocessspanattaching-to-a-running-process"></a><span id="Attaching_to_a_Running_Process"></span><span id="attaching_to_a_running_process"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS"></span>将附加到正在运行的进程


### <a name="span-idcommandprompt1spanspan-idcommandprompt1spancommand-prompt"></a><span id="command_prompt1"></span><span id="COMMAND_PROMPT1"></span>命令提示符

在命令提示符窗口中，您可以将附加到正在运行的进程启动 CDB 时。 使用以下命令之一：

-   **cdb -p** *ProcessID*
-   **cdb -pn** *ProcessName*

其中*ProcessID*是正在运行的进程的进程 ID 或*ProcessName*是正在运行的进程的名称。

有关命令行语法的详细信息，请参阅[ **CDB 命令行选项**](cdb-command-line-options.md)。

### <a name="span-idcdbcommandwindow1spanspan-idcdbcommandwindow1spancdb-command-window"></a><span id="cdb_command_window1"></span><span id="CDB_COMMAND_WINDOW1"></span>CDB 命令窗口

如果调试器已调试一个或多个进程，则可以通过使用附加到正在运行的进程[ **.attach （附加到进程）** ](-attach--attach-to-process-.md)命令。

调试器始终启动多个目标进程同时，除非它们的线程的一些被冻结或挂起。

如果[ **.attach** ](-attach--attach-to-process-.md)命令成功，将调试器附加到指定的进程发出执行命令，在调试器下一次。 如果行中多次使用此命令，必须请求无数次，使用此命令在调试器的执行。

## <a name="span-idattachingtoarunningprocessnoninvasivelyspanspan-idattachingtoarunningprocessnoninvasivelyspanspan-idattachingtoarunningprocessnoninvasivelyspanattaching-to-a-running-process-noninvasively"></a><span id="Attaching_to_a_Running_Process_Noninvasively"></span><span id="attaching_to_a_running_process_noninvasively"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_NONINVASIVELY"></span>Noninvasively 附加到正在运行的进程


如果你想要调试正在运行的进程，仅在最低程度会影响在其执行中，应调试进程[noninvasively](noninvasive-debugging--user-mode-.md)。

### <a name="span-idcommandprompt2spanspan-idcommandprompt2spancommand-prompt"></a><span id="command_prompt2"></span><span id="COMMAND_PROMPT2"></span>命令提示符

若要 noninvasively 调试正在运行的进程 CDB 命令行中，指定 **-pv**选项， **-p**选项和进程 ID，在下面的语法。

**cdb -pv -p** *ProcessID*

或者，若要通过指定进程名称 noninvasively 调试正在运行的进程，请改为使用以下语法。

**cdb -pv -pn** *ProcessName*

有几个其他有用的命令行选项。 有关命令行语法的详细信息，请参阅[ **CDB 命令行选项**](cdb-command-line-options.md)。

### <a name="span-idcdbcommandwindow2spanspan-idcdbcommandwindow2spancdb-command-window"></a><span id="cdb_command_window2"></span><span id="CDB_COMMAND_WINDOW2"></span>CDB 命令窗口

如果调试器已处于活动状态，可以通过输入 noninvasively 调试正在运行的进程[ **.attach-v （附加到进程）** ](-attach--attach-to-process-.md)命令。

可以使用 **.attach**命令如果调试程序已调试一个或多个进程 invasively。

如果 **.attach v**命令成功，调试器将调试指定的进程发出执行命令，在调试器下一次。 在非侵入调试过程中不允许执行，因为调试器不能 noninvasively 调试一次的多个进程。 此限制也意味着，使用 **.attach v**命令可能会使现有的侵入性调试会话不太有用。

## <a name="span-idspawninganewprocessspanspan-idspawninganewprocessspanspan-idspawninganewprocessspanspawning-a-new-process"></a><span id="Spawning_a_New_Process"></span><span id="spawning_a_new_process"></span><span id="SPAWNING_A_NEW_PROCESS"></span>生成新的进程


CDB 可以启动在用户模式应用程序和调试应用程序。 按名称指定应用程序。 可以还会自动将调试器附加到子进程 （原始目标进程启动的其他进程） 中。

调试器创建 （也称为生成的进程） 的进程的行为略有不同的调试器不会创建进程。

而不是使用标准堆 API，调试器创建的进程使用特殊的调试堆。 你可以强制执行生成的进程，而不是调试堆中通过使用标准堆\_否\_调试\_堆[环境变量](general-environment-variables.md)或 **-hd**命令行选项。

此外，由于目标应用程序是在调试器的子进程，它将继承的调试程序的权限。 此权限可能会使目标应用程序来执行其否则无法执行某些操作。 例如，目标应用程序可能能够影响受保护的进程。

在命令提示符窗口中，可以启动 CDB 时生成一个新的进程。 输入以下命令。

**cdb \[-o\]** *ProgramName* **\[**<em>Arguments</em>**\]**

**-O**选项将使调试器附加到子进程。 有几个其他有用的命令行选项。 有关命令行语法的详细信息，请参阅[ **CDB 命令行选项**](cdb-command-line-options.md)。

如果调试器已调试一个或多个进程，则可以通过输入创建新进程[ **.create （创建进程）** ](-create--create-process-.md)命令。

除非一些其线程被冻结或挂起调试器始终将同时启动多个目标进程。

如果[ **.create** ](-create--create-process-.md)命令成功，调试器将会发出执行命令时，调试器都会创建指定的进程。 如果行中多次使用此命令，必须请求无数次，使用此命令在调试器的执行。

你可以通过使用控制应用程序的开始目录[ **.createdir （设置创建的进程目录）** ](-createdir--set-created-process-directory-.md)命令之前[ **.create** ](-create--create-process-.md). 可以使用 **.createdir-我**命令或 **-noinh**命令行选项来控制目标应用程序是否继承调试器的句柄。

可以激活或停用使用调试子进程[ **.childdbg （调试子进程）** ](-childdbg--debug-child-processes-.md)命令。

## <a name="span-idreattachingtoaprocessspanspan-idreattachingtoaprocessspanspan-idreattachingtoaprocessspanreattaching-to-a-process"></a><span id="Reattaching_to_a_Process"></span><span id="reattaching_to_a_process"></span><span id="REATTACHING_TO_A_PROCESS"></span>重新附加到进程


如果在调试器停止响应或会冻结，您可以将新的调试器附加到目标进程。 有关如何附加调试器在这种情况的详细信息，请参阅[重新附加到目标应用程序](reattaching-to-the-target-application.md)。

 

 





