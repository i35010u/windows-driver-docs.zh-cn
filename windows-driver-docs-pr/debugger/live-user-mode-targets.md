---
title: 实时用户模式目标
description: 实时用户模式目标
ms.assetid: 2709dd01-6486-471d-afa1-a8441665da8d
keywords:
- 调试器引擎 API、 目标、 用户模式
- 调试器引擎 API，从进程断开连接
- 调试器引擎 API，处理选项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77e8334d317a916dd397891b8e77dbbee142c7ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542539"
---
# <a name="live-user-mode-targets"></a>实时用户模式目标


## <span id="ddk_live_user_mode_targets_dbx"></span><span id="DDK_LIVE_USER_MODE_TARGETS_DBX"></span>


本地计算机和远程计算机运行的进程服务器，可用于创建和附加到本主题中列出的进程的方法。

可以使用创建用户模式进程[**创建流程**](https://msdn.microsoft.com/library/windows/hardware/ff539321)或[ **CreateProcess2**](https://msdn.microsoft.com/library/windows/hardware/ff539323)，其执行给定的命令，创建过程。 该方法[ **AttachProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff538150)可用于将附加[调试器引擎](introduction.md#debugger-engine)到现有用户模式进程。 [**CreateProcessAndAttach** ](https://msdn.microsoft.com/library/windows/hardware/ff540048)并[ **CreateProcessAndAttach2** ](https://msdn.microsoft.com/library/windows/hardware/ff540055)创建一个新的用户模式进程并附加到它或同一台计算机上的另一个用户模式进程。 [**请求**](https://msdn.microsoft.com/library/windows/hardware/ff554564) operations [**调试\_请求\_GET\_其他\_创建\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff541553)， [**调试\_请求\_设置\_其他\_创建\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff541586)，并[**调试\_请求\_设置\_本地\_隐式\_命令\_行**](https://msdn.microsoft.com/library/windows/hardware/ff541592)可以用于设置一些用于创建进程的默认选项。

**请注意**  引擎完全不会附加到进程中，直到[ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)调用方法。 仅在过程具有生成的事件-例如，进程创建事件-后实际上它已成为在调试器会话中可用。 请参阅[调试会话和执行模型](debugging-session-and-execution-model.md)的更多详细信息。

 

该方法[ **GetRunningProcessSystemIds** ](https://msdn.microsoft.com/library/windows/hardware/ff548265)将返回计算机上的进程正在运行的所有进程的 Id。 可以使用查找特定程序的进程 ID [ **GetRunningProcessSystemIdByExecutableName**](https://msdn.microsoft.com/library/windows/hardware/ff548254)。 给定进程 ID，由返回过程的说明[ **GetRunningProcessDescription**](https://msdn.microsoft.com/library/windows/hardware/ff548243)。

### <a name="span-idprocessoptionsspanspan-idprocessoptionsspanspan-idprocessoptionsspanprocess-options"></a><span id="Process_Options"></span><span id="process_options"></span><span id="PROCESS_OPTIONS"></span>处理选项

处理选项确定引擎的行为时附加到用户模式进程，包括调试器引擎会自动附加到创建的目标进程且引擎不会与目标的子进程的一部分进程退出时。 请参阅[**调试\_进程\_XXX** ](https://msdn.microsoft.com/library/windows/hardware/ff541534)有关处理选项的说明。

可以使用查询处理选项[ **GetProcessOptions**](https://msdn.microsoft.com/library/windows/hardware/ff548163)。 可以使用更改他们[ **AddProcessOptions**](https://msdn.microsoft.com/library/windows/hardware/ff537917)， [ **RemoveProcessOptions**](https://msdn.microsoft.com/library/windows/hardware/ff554505)，并[ **SetProcessOptions**](https://msdn.microsoft.com/library/windows/hardware/ff556765)。

### <a name="span-iddisconnectingfromprocessesspanspan-iddisconnectingfromprocessesspanspan-iddisconnectingfromprocessesspandisconnecting-from-processes"></a><span id="Disconnecting_from_Processes"></span><span id="disconnecting_from_processes"></span><span id="DISCONNECTING_FROM_PROCESSES"></span>从进程断开连接

有三种不同方法要从进程断开连接的引擎。

1.  *分离*。 恢复过程中的所有线程，以便它将继续运行，无法再进行调试。 [**DetachCurrentProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff541846)将分离当前进程中的引擎和[ **DetachProcesses** ](https://msdn.microsoft.com/library/windows/hardware/ff541851)将分离与所有进程引擎。 并非所有目标都支持分离。 [**请求**](https://msdn.microsoft.com/library/windows/hardware/ff554564)操作[**调试\_请求\_目标\_可以\_分离**](https://msdn.microsoft.com/library/windows/hardware/ff541602)可用于检查目标是否支持分离。

2.  *终止*。 尝试终止该进程。 [**TerminateCurrentProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff558866)将终止当前进程并[ **TerminateProcesses** ](https://msdn.microsoft.com/library/windows/hardware/ff558867)调试器会话将终止所有进程。

3.  *放弃*。 从正在调试的进程列表中删除该过程。 操作系统将仍会考虑与正在调试进程，它将保持挂起状态直到另一个调试器附加到它或它的过程中终止。 [**AbandonCurrentProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff537786)将放弃当前进程。

 

 





