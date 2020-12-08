---
title: 解决 TraceView 错误
description: 解决 TraceView 错误
keywords:
- TraceView WDK，错误
- 错误 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6ca3f6e0d7b66a87191c9b8fcbc04fad0d72f6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839739"
---
# <a name="resolving-traceview-errors"></a>解决 TraceView 错误

本主题介绍 TraceView 常见报告和建议解决方案的错误。 这并不是一个完整的故障排除指南。

### <a name="span-idtrace_provider_is_not_addedspanspan-idtrace_provider_is_not_addedspantrace-provider-is-not-added"></a><span id="trace_provider_is_not_added"></span><span id="TRACE_PROVIDER_IS_NOT_ADDED"></span>未添加跟踪提供程序

如果 TraceView 无法找到跟踪提供程序的 [PDB 符号文件](pdb-symbol-files.md) 或 [跟踪消息格式 (. tmf) 文件](trace-message-format-file.md) ，则它不会将跟踪提供程序添加到 " **创建新的日志会话** " 对话框中的提供程序列表，也不会显示一条消息，说明未添加提供程序的原因。

如果在您尝试添加提供程序后，该提供程序未显示在提供程序列表中，则重新启动该过程，然后在 "设置 **信息源格式** " 对话框中，单击 " **选择 TMF 文件** 而不是 **设置 TMF 搜索路径**"。 如果找不到提供程序的 PDB 文件或 TMF 文件，则不能使用 TraceView 创建与提供程序的跟踪会话。

### <a name="span-idfailed_to_enable_trace_for_control_guid__guidspanspan-idfailed_to_enable_trace_for_control_guid__guidspanfailed-to-enable-trace-for-control-guid-guid"></a><span id="failed_to_enable_trace_for_control_guid__guid"></span><span id="FAILED_TO_ENABLE_TRACE_FOR_CONTROL_GUID__GUID"></span>未能为控件 GUID： *Guid* 启用跟踪

当多个跟踪使用者在系统上的单个跟踪提供程序中收集事件时，通常会发生此错误。 若要解决此冲突，请显示计算机上正在运行的所有跟踪会话，并停止发生冲突的会话。

若要在计算机上显示所有跟踪会话，请在命令提示符窗口中键入 **traceview-l**。  ("TraceView" 窗口仅显示在 TraceView 中运行的跟踪会话。 ) 生成的显示将列出活动会话。

若要停止跟踪会话，请在命令提示符窗口中键入 **traceview-stop**_SessionName_。

有关这些命令的详细信息，请参阅 [**TraceView Control 命令**](traceview-control-commands.md)。

### <a name="span-idcannot_open_logfile_for_readingspanspan-idcannot_open_logfile_for_readingspancannot-open-logfile-for-reading"></a><span id="cannot_open_logfile_for_reading"></span><span id="CANNOT_OPEN_LOGFILE_FOR_READING"></span>无法打开要读取的日志文件

当你尝试为跟踪提供程序显示一个现有跟踪日志，该跟踪提供程序为实时跟踪会话或 TraceView 中的另一个现有跟踪日志提供事件时，会发生此错误。

### <a name="span-idcannot_connect_to_any_trace_session_in_the_groupspanspan-idcannot_connect_to_any_trace_session_in_the_groupspancannot-connect-to-any-trace-session-in-the-group"></a><span id="cannot_connect_to_any_trace_session_in_the_group"></span><span id="CANNOT_CONNECT_TO_ANY_TRACE_SESSION_IN_THE_GROUP"></span>无法连接到组中的任何跟踪会话

若要解决此错误，请查看分组主题的 [限制](limitations-of-grouping.md) ，并仅包含可以在系统上分组的跟踪会话。

### <a name="span-idinternal_error__closetrace_error_170spanspan-idinternal_error__closetrace_error_170spaninternal-error-closetrace-error-170"></a><span id="internal_error__closetrace_error_170"></span><span id="INTERNAL_ERROR__CLOSETRACE_ERROR_170"></span>内部错误： CloseTrace 错误170

当你尝试加入已经正在进行的 NT 内核记录器跟踪会话时，将出现此错误。 你可以使用 TraceView 来创建 NT 内核记录器跟踪会话，但不能加入由 TraceView 以外的工具或方法启动的 NT 内核记录器跟踪会话。

有关详细信息，请参阅 [联接跟踪会话](joining-a-trace-session.md) 和 [创建 NT 内核记录器跟踪会话](creating-an-nt-kernel-logger-trace-session.md)。
