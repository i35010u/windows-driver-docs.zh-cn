---
title: 实时用户模式目标
description: 实时用户模式目标
ms.assetid: 2709dd01-6486-471d-afa1-a8441665da8d
keywords:
- 调试器引擎 API，目标，用户模式
- 调试器引擎 API，从进程断开连接
- 调试器引擎 API，处理选项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143d8c1e026d6c1928835f4c914601d956a9fb13
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534340"
---
# <a name="live-user-mode-targets"></a>实时用户模式目标


## <span id="ddk_live_user_mode_targets_dbx"></span><span id="DDK_LIVE_USER_MODE_TARGETS_DBX"></span>


用于创建和附加到本主题中列出的进程的方法可用于本地计算机和运行进程服务器的远程计算机。

用户模式进程可以使用[**Create process**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)或[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)创建，后者执行给定的命令来创建进程。 方法[**AttachProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-attachprocess)可用于将[调试器引擎](introduction.md#debugger-engine)附加到现有的用户模式进程。 [**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)和[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)创建新的用户模式进程，并将其附加到同一台计算机上或其他用户模式进程。 [**请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**调试 \_ 请求 \_ 获取 \_ 其他 \_ 创建 \_ 选项**](debug-request-get-additional-create-options.md)、[**调试 \_ 请求 \_ 设置 \_ 附加 \_ 创建 \_ 选项**](debug-request-set-additional-create-options.md)和[**调试 \_ 请求 \_ 集 \_ 本地 \_ 隐式 \_ 命令 \_ 行**](debug-request-set-local-implicit-command-line.md)可用于设置某些用于创建进程的默认选项。

**注意**   在调用[**WaitForEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)方法之前，引擎不会完全附加到进程。 只有在进程生成事件（例如进程创建事件）后，它才会在调试器会话中可用。 有关更多详细信息，请参阅[调试会话和执行模型](debugging-session-and-execution-model.md)。

 

方法[**GetRunningProcessSystemIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getrunningprocesssystemids)将返回计算机上所有正在运行的进程的进程 id。 可以使用[**GetRunningProcessSystemIdByExecutableName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getrunningprocesssystemidbyexecutablename)查找特定程序的进程 ID。 给定进程 ID 后， [**GetRunningProcessDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getrunningprocessdescription)将返回进程的描述。

### <a name="span-idprocess_optionsspanspan-idprocess_optionsspanspan-idprocess_optionsspanprocess-options"></a><span id="Process_Options"></span><span id="process_options"></span><span id="PROCESS_OPTIONS"></span>处理选项

处理选项在附加到用户模式进程时确定引擎的部分行为，包括调试器引擎是否将自动附加到目标进程创建的子进程，以及引擎在退出时如何处理目标进程。 有关进程选项的说明，请参阅[**调试 \_ 过程 \_ XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-process-xxx) 。

可以使用[**GetProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getprocessoptions)查询处理选项。 可使用[**AddProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-addprocessoptions)、 [**RemoveProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-removeprocessoptions)和[**SetProcessOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setprocessoptions)更改它们。

### <a name="span-iddisconnecting_from_processesspanspan-iddisconnecting_from_processesspanspan-iddisconnecting_from_processesspandisconnecting-from-processes"></a><span id="Disconnecting_from_Processes"></span><span id="disconnecting_from_processes"></span><span id="DISCONNECTING_FROM_PROCESSES"></span>与进程断开连接

引擎可以使用三种不同的方法从进程断开连接。

1.  *分离*。 恢复进程中的所有线程，以便它将继续运行，不再进行调试。 [**DetachCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-detachcurrentprocess)将从当前进程分离引擎， [**DetachProcesses**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-detachprocesses)将从所有进程分离引擎。 并非所有目标都支持分离。 可以使用 "[**请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request)操作"[**调试 \_ 请求 \_ 目标 \_ \_ **](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-can-detach)来检查目标是否支持分离。

2.  *终止*。 尝试终止进程。 [**TerminateCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-terminatecurrentprocess)将终止当前进程，并且[**TerminateProcesses**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-terminateprocesses)将终止调试器会话中的所有进程。

3.  *放弃*。 从正在调试的进程列表中删除该进程。 操作系统仍会将进程视为已被调试，并且它将保持挂起状态，直到另一个调试器附加到它或被终止。 [**AbandonCurrentProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-abandoncurrentprocess)将放弃当前进程。

 

 





