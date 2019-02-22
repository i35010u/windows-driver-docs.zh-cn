---
title: 加入跟踪会话
description: 加入跟踪会话
ms.assetid: 0fd065e4-004f-426a-bdb1-4b2e7d219e20
keywords:
- 跟踪会话 WDK，联接
- 跟踪 WDK，正在进行的会话
- 正在跟踪会话 WDK
- 软件跟踪 WDK，正在进行中的会话
- 停止跟踪会话
- 正在取消跟踪会话
- 重新启动跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c39e5d0516054ab13dffff2e12705e20b23c92f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554698"
---
# <a name="joining-a-trace-session"></a>加入跟踪会话


在极少数情况下，例如时强制 TraceView 退出时用于控制正在运行的跟踪会话，TraceView 不禁用会话提供程序，并停止跟踪会话。 在这种情况下，当你尝试使用的提供程序仍处于启用状态，启动跟踪会话时 TraceView 显示一条警告并提供停止并重新启动会话，或可加入已在进行跟踪会话。

在对话框中的选项如下所示：

<span id="Yes_-_Stop_and_Restart_the_Log_Session"></span><span id="yes_-_stop_and_restart_the_log_session"></span><span id="YES_-_STOP_AND_RESTART_THE_LOG_SESSION"></span>**是-停止并重新启动日志会话**  
TraceView 停止跟踪会话，然后启动新的跟踪会话使用相同的提供程序和相同的属性。

<span id="No_-_Join_the_Log_Session_Without_Stopping"></span><span id="no_-_join_the_log_session_without_stopping"></span><span id="NO_-_JOIN_THE_LOG_SESSION_WITHOUT_STOPPING"></span>**否-加入不间断的日志会话**  
TraceView 检索和保存会话属性和联接跟踪会话。 您可以使用 TraceView 更改跟踪会话的属性，但 TraceView 无法停止跟踪会话。 若要停止跟踪会话[退出 TraceView](starting-and-exiting-traceview.md)。

<span id="Cancel_-_Abort_Start_Operation"></span><span id="cancel_-_abort_start_operation"></span><span id="CANCEL_-_ABORT_START_OPERATION"></span>**取消按钮-中止开始操作**  
TraceView 取消尝试启动跟踪会话。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

TraceView 窗口显示只有那些运行它启动跟踪会话。 若要列出在系统运行的所有跟踪会话，请键入**traceview-l**在命令提示符窗口中。 若要停止跟踪会话 TraceView 未启动的请键入 **traceview-停止 * * * SessionName*在命令提示符窗口中。 有关这些命令的详细信息，请参阅[TraceView 命令行界面](traceview-command-line-interface.md)。

 

 





