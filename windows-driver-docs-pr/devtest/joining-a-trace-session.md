---
title: 加入跟踪会话
description: 加入跟踪会话
keywords:
- 跟踪会话 WDK，加入
- 跟踪 WDK，正在进行的会话
- 正在进行的跟踪会话 WDK
- 软件跟踪 WDK，正在进行的会话
- 停止跟踪会话
- 取消跟踪会话
- 重新启动跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52d9741f1617a0fbac914d8f4b688171df4b102
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806485"
---
# <a name="joining-a-trace-session"></a>加入跟踪会话


在极少数情况下（例如当你强制 TraceView 在控制正在运行的跟踪会话时退出）时，TraceView 不会禁用会话提供程序，也不会停止跟踪会话。 在这种情况下，当你尝试使用仍处于启用状态的提供程序启动跟踪会话时，TraceView 将显示一个警告，并提供停止并重新启动该会话的通知，或者让你加入已在进行中的跟踪会话。

此对话框中的选项如下所示：

<span id="Yes_-_Stop_and_Restart_the_Log_Session"></span><span id="yes_-_stop_and_restart_the_log_session"></span><span id="YES_-_STOP_AND_RESTART_THE_LOG_SESSION"></span>**是-停止并重新启动日志会话**  
TraceView 停止跟踪会话，然后使用相同的提供程序和属性启动新的跟踪会话。

<span id="No_-_Join_the_Log_Session_Without_Stopping"></span><span id="no_-_join_the_log_session_without_stopping"></span><span id="NO_-_JOIN_THE_LOG_SESSION_WITHOUT_STOPPING"></span>**否-无需停止即可联接日志会话**  
TraceView 检索并保存会话属性，并联接跟踪会话。 您可以使用 TraceView 更改跟踪会话的属性，但 TraceView 无法停止跟踪会话。 若要停止跟踪会话，请 [退出 TraceView](starting-and-exiting-traceview.md)。

<span id="Cancel_-_Abort_Start_Operation"></span><span id="cancel_-_abort_start_operation"></span><span id="CANCEL_-_ABORT_START_OPERATION"></span>**取消-中止启动操作**  
TraceView 取消启动跟踪会话的尝试。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

"TraceView" 窗口仅显示启动的跟踪会话。 若要列出系统上运行的所有跟踪会话，请在命令提示符窗口中键入 **traceview-l** 。 若要停止 TraceView 未启动的跟踪会话，请在命令提示符窗口中键入 **TraceView-stop**_SessionName_ 。 有关这些命令的详细信息，请参阅 [TraceView Command-Line Interface](traceview-command-line-interface.md)。

 

 





