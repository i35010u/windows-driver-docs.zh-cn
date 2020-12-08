---
title: 查找进程 ID
description: 查找进程 ID
keywords:
- '进程 ID (PID) '
- 'PID (进程 ID) '
- Tlist.exe，相关技术
- 任务管理器
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 90b7fbf073cb058126570019468d52634667e1aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838187"
---
# <a name="finding-the-process-id"></a>查找进程 ID


## <span id="ddk_finding_the_process_id_dbg"></span><span id="DDK_FINDING_THE_PROCESS_ID_DBG"></span>


为 Microsoft Windows 中运行的每个进程分配一个唯一的十进制数，称为进程 ID (PID) 。 此数字用于指定在将调试器附加到进程时的进程。

您可以使用任务管理器、 **tasklist** 命令、tlist.exe 实用工具或调试器来确定给定应用程序的 PID。

## <a name="span-idtask_managerspanspan-idtask_managerspantask-manager"></a><span id="task_manager"></span><span id="TASK_MANAGER"></span>任务管理器

可以通过多种方法打开任务管理器，但最简单的方法是选择 Ctrl + Alt + Delete，然后选择 " **任务管理器**"。

在 " **进程** " 选项卡上，选择 " **详细信息** " 以查看 PID 以及其他有用的信息。

某些内核错误可能会导致任务管理器的图形界面发生延迟。

## <a name="span-idthe_tasklist_commandspanspan-idthe_tasklist_commandspanthe-tasklist-command"></a><span id="the_tasklist_command"></span><span id="THE_TASKLIST_COMMAND"></span>**Tasklist** 命令

在命令提示符下使用 **tasklist** 命令显示所有进程、其 pid 以及各种其他详细信息。

## <a name="span-idtlistspanspan-idtlistspantlist-utility"></a><span id="tlist"></span><span id="TLIST"></span>Tlist.exe 实用程序

任务列表查看器 (Tlist.exe) 或 tlist.exe 是一个命令行实用工具，用于显示当前在本地计算机上运行的任务列表或用户模式进程。 Tlist.exe 包含在 Windows 的调试工具包中。

当你从命令提示符运行 Tlist.exe 时，它将在内存中显示具有唯一 PID 号的所有用户模式进程的列表。 对于每个进程，它将显示 PID、进程名称和，如果进程具有窗口，则显示该窗口的标题。

有关详细信息，请参阅 [tlist.exe](tlist.md)。

## <a name="span-idthe__tlist_debugger_commandspanspan-idthe__tlist_debugger_commandspanthe-tlist-debugger-command"></a><span id="the__tlist_debugger_command"></span><span id="THE__TLIST_DEBUGGER_COMMAND"></span>**Tlist.exe** 调试器命令

如果在相关系统上已经有一个用户模式调试器在运行，则 [**tlist.exe (列出进程 id)**](-tlist--list-process-ids-.md) 命令将显示该系统上所有 pid 的列表。

## <a name="span-idcsrss_and_user_mode_driversspanspan-idcsrss_and_user_mode_driversspancsrss-and-user-mode-drivers"></a><span id="csrss_and_user_mode_drivers"></span><span id="CSRSS_AND_USER_MODE_DRIVERS"></span>CSRSS 和用户模式驱动程序

若要调试在另一台计算机上运行的用户模式驱动程序，请 Run-Time 子系统 (CSRSS) 进程中调试客户端服务器。 有关详细信息，请参阅 [调试 CSRSS](debugging-csrss.md)。

 

 





