---
title: 基本跟踪会话选项
description: 基本跟踪会话选项
keywords:
- 跟踪会话 WDK，基本选项
- 跟踪 WDK，基本选项
- 软件跟踪 WDK，基本选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f40b35dbae37e2ed58a97793fda1f2d41b4c51a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803595"
---
# <a name="basic-trace-session-options"></a>基本跟踪会话选项

以下列表描述了可以在 " **日志会话选项** " 页上更改的基本跟踪会话选项。

<span id="Real_Time_Display"></span><span id="real_time_display"></span><span id="REAL_TIME_DISPLAY"></span>**实时显示**  
创建 [实时跟踪会话](trace-session.md#ddk_real_time_trace_sessions_tools)。默认情况下，此选项处于选中状态。

您必须选择 **"将跟踪事件数据记录到文件" 和/或 "实时显示**"。

<span id="Log_Session_Name"></span><span id="log_session_name"></span><span id="LOG_SESSION_NAME"></span>**日志会话名称**  
指定跟踪会话的名称。 选择符合 Windows 命名标准的任意名称，最多1024个字符。 默认值为 "LogSession *n*"，其中 *N* 是一个从零开始的整数，它表示会话的创建顺序。

为跟踪会话命名后，可以通过其名称引用会话 (例如，在使用 [TraceView 命令行接口](traceview-command-line-interface.md)) 时。

<span id="Log_Trace_Event_Data_To_File__"></span><span id="log_trace_event_data_to_file__"></span><span id="LOG_TRACE_EVENT_DATA_TO_FILE__"></span>**将跟踪事件数据记录到文件**   
创建 [跟踪日志会话](trace-session.md#ddk_trace_log_sessions_tools)。

您必须选择 " **将跟踪事件数据记录到文件**" 和/或 " **实时显示**"。

<span id="Log_File_Name"></span><span id="log_file_name"></span><span id="LOG_FILE_NAME"></span>**日志文件名**  
指定 [跟踪日志](trace-log.md) ( .etl) 的路径和文件名。 仅当选择了 "将 **日志跟踪事件数据到文件** " 选项时，才会启用此选项。

默认情况下，跟踪日志的名称为 "LogSession<em> \_ date \_ time</em>.etl"，并保存在本地目录中。 若要更改名称或位置，请在文本框中键入路径和文件名，或单击省略号按钮 " ( ..." ) 。

> [!CAUTION]
> 如果选择现有文件的路径和名称，TraceView 将在不发出警告的情况下覆盖该文件。

<span id="Append_To_Existing_Log_File"></span><span id="append_to_existing_log_file"></span><span id="APPEND_TO_EXISTING_LOG_FILE"></span>**追加到现有日志文件**  
将跟踪消息添加到 " **日志文件名** " 框中指定的跟踪日志文件的末尾，而不是覆盖该文件。

仅当启用了 " **将跟踪事件数据记录到文件** " 且禁用了 **实时显示** 时，才会启用此选项。 不能将实时事件追加到现有的跟踪日志。

TraceView 使您可以选择此选项，即使指定的文件尚不存在也是如此。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

跟踪会话名称并不保存在事件跟踪日志 ( .etl) 文件、TraceView 输出文件或 TraceView 摘要文件中。 当你使用 TraceView 显示跟踪日志时，它将使用默认会话名称 "LogSession *N*" 作为跟踪会话的名称，其中 *N* 是一个从零开始的整数，它表示会话的创建顺序。
