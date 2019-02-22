---
title: 基本跟踪会话选项
description: 基本跟踪会话选项
ms.assetid: c997310f-79dc-4c94-945e-13a0a7786928
keywords:
- 跟踪会话 WDK，基本选项
- 跟踪 WDK，基本选项
- 软件跟踪 WDK，基本选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 042d6252918efb7dc3755333855eefe354ab138a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523155"
---
# <a name="basic-trace-session-options"></a>基本跟踪会话选项

以下列表描述了你可以在基本跟踪会话选项**日志会话选项**页。

<span id="Real_Time_Display"></span><span id="real_time_display"></span><span id="REAL_TIME_DISPLAY"></span>**实时显示**  
创建[实时跟踪会话](trace-session.md#ddk_real_time_trace_sessions_tools)。默认情况下选择此选项。

必须选择**日志跟踪事件数据到文件、 实时显示**，和 / 或。

<span id="Log_Session_Name"></span><span id="log_session_name"></span><span id="LOG_SESSION_NAME"></span>**日志会话名称**  
指定跟踪会话的名称。 选择满足 Windows 命名标准，最多 1024年个字符的任何名称。 默认值是"LogSession*N*"，其中*N*是一个从零开始的整数，它表示在其中创建该会话的顺序。

在命名跟踪会话后，你可以引用会话按其名称 (例如，当您使用[TraceView 命令行界面](traceview-command-line-interface.md))。

<span id="Log_Trace_Event_Data_To_File__"></span><span id="log_trace_event_data_to_file__"></span><span id="LOG_TRACE_EVENT_DATA_TO_FILE__"></span>**日志文件的跟踪事件数据**   
创建[跟踪日志会话](trace-session.md#ddk_trace_log_sessions_tools)。

必须选择**日志跟踪事件数据到文件**，**实时显示**，和 / 或。

<span id="Log_File_Name"></span><span id="log_file_name"></span><span id="LOG_FILE_NAME"></span>**日志文件名称**  
指定的路径和文件名称[跟踪日志](trace-log.md)(.etl)。 启用此选项时，才**日志跟踪事件数据到文件**选择选项。

默认情况下，跟踪日志命名为"LogSession<em>\_日期\_时间</em>.etl"，保存在本地目录。 若要更改名称或位置、 在文本框中键入路径和文件名，或若要导航到目录中，单击省略号按钮 （...）。

> [!CAUTION]
> 如果您选择的路径和名称的现有文件，TraceView 将覆盖该文件而不发出警告。

<span id="Append_To_Existing_Log_File"></span><span id="append_to_existing_log_file"></span><span id="APPEND_TO_EXISTING_LOG_FILE"></span>**追加到现有日志文件**  
将跟踪消息添加到跟踪日志文件中指定的最终**日志文件名称**框中的，而不是覆盖该文件。

启用此选项时，才**日志跟踪事件数据到文件**已启用并**实时显示**被禁用。 不能将实时事件追加到现有的跟踪日志。

TraceView 允许您选择此选项，即使指定的文件尚不存在。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

跟踪日志 (.etl) 文件、 TraceView 输出文件或 TraceView 摘要文件，并不在事件保存跟踪会话名称。 当 TraceView 用于显示跟踪日志时，它使用默认的会话名称，"LogSession*N*"作为名称跟踪会话，其中*N*是一个从零开始的整数，它表示的顺序创建会话。
