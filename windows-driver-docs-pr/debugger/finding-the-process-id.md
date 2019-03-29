---
title: 查找进程 ID
description: 查找进程 ID
ms.assetid: 963e9b5b-2b88-41b5-a103-dc4611ff41ea
keywords:
- 进程的进程 ID (PID)
- PID (进程 ID)
- TList，相关技术
- 任务管理器
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2add0a5362e6f9bbadf0fdddbc464c7cda144d02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569174"
---
# <a name="finding-the-process-id"></a>查找进程 ID


## <span id="ddk_finding_the_process_id_dbg"></span><span id="DDK_FINDING_THE_PROCESS_ID_DBG"></span>


在 Microsoft Windows 中运行每个进程分配唯一的十进制数字，称为*进程 ID*，或*PID*。 此数值用于指定的进程时将调试器附加到它。

有几种方法来确定给定应用程序的 PID： 使用任务管理器，并使用**tasklist**使用 TList 实用程序，或使用调试器命令。

### <a name="span-idtaskmanagerspanspan-idtaskmanagerspantask-manager"></a><span id="task_manager"></span><span id="TASK_MANAGER"></span>任务管理器

*任务管理器*可能激活中通过多种方式，但最简单的是，若要按 CTRL + ALT + DELETE，然后单击**任务管理器**。

从**进程**选项卡上，单击**详细信息**选项卡以查看该 PID，以及其他有用信息。

在任务管理器的图形界面中，某些内核错误可能会导致延迟。

### <a name="span-idthetasklistcommandspanspan-idthetasklistcommandspanthe-tasklist-command"></a><span id="the_tasklist_command"></span><span id="THE_TASKLIST_COMMAND"></span>Tasklist 命令

使用**tasklist**命令从命令提示符窗口以显示所有进程、 Pid 和各种其他详细信息。

### <a name="span-idtlistspanspan-idtlistspantlist"></a><span id="tlist"></span><span id="TLIST"></span>TList

TList （任务列表查看器，tlist.exe） 是一个命令行实用工具，显示的任务或在本地计算机上当前运行的用户模式进程列表。 TList 是有关 Windows 调试工具软件包中包含的。

当从命令提示符处运行 TList 时，它将以与唯一进程标识号 (PID) 的内存中显示的所有用户模式进程的列表。 对于每个进程，它显示 PID 的进程名称，并且该过程有一个窗口，该窗口的标题。

有关详细信息，请参阅[TList](tlist.md)。

### <a name="span-idthetlistdebuggercommandspanspan-idthetlistdebuggercommandspanthe-tlist-debugger-command"></a><span id="the__tlist_debugger_command"></span><span id="THE__TLIST_DEBUGGER_COMMAND"></span>.Tlist 调试器命令

如果已存在，系统上运行的用户模式下调试程序[ **.tlist (列表进程 Id)** ](-tlist--list-process-ids-.md)命令将显示该系统上的所有 Pid 的列表。

### <a name="span-idcsrssandusermodedriversspanspan-idcsrssandusermodedriversspancsrss-and-user-mode-drivers"></a><span id="csrss_and_user_mode_drivers"></span><span id="CSRSS_AND_USER_MODE_DRIVERS"></span>CSRSS 和用户模式驱动程序

若要调试在另一台计算机上运行的用户模式驱动程序，调试客户端服务器运行时子系统 (CSRSS) 进程。 有关详细信息，请参阅[调试 CSRSS](debugging-csrss.md)。

 

 





