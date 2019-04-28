---
title: 解决 TraceView 错误
description: 解决 TraceView 错误
ms.assetid: 4849e0b6-5dc9-4666-b1ca-ec89cb94bed0
keywords:
- TraceView WDK 错误
- 错误 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d82be9f0bf8de5bd34c786ff6a60c4809e9d9c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340264"
---
# <a name="resolving-traceview-errors"></a>解决 TraceView 错误

本主题介绍错误 TraceView 通常报告并建议解决方案。 不应为完整的故障排除指南。

### <a name="span-idtraceproviderisnotaddedspanspan-idtraceproviderisnotaddedspantrace-provider-is-not-added"></a><span id="trace_provider_is_not_added"></span><span id="TRACE_PROVIDER_IS_NOT_ADDED"></span>不添加跟踪提供程序

如果找不到 TraceView [PDB 符号文件](pdb-symbol-files.md)或[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)跟踪提供程序，它向提供程序列表中不添加跟踪提供程序**新建日志会话**对话框中，并且它不显示一条消息，说明为何未添加提供程序。

如果在尝试将其添加，重新开始该过程后将提供程序列表中，并在提供程序未出现**格式的信息源选择**对话框中，单击**选择 TMF 文件**而不是**TMF 搜索路径设置**。 如果您找不到提供程序的 PDB 文件或 TMF 文件，则无法使用 TraceView 与提供程序创建跟踪会话。

### <a name="span-idfailedtoenabletraceforcontrolguidguidspanspan-idfailedtoenabletraceforcontrolguidguidspanfailed-to-enable-trace-for-control-guid-guid"></a><span id="failed_to_enable_trace_for_control_guid__guid"></span><span id="FAILED_TO_ENABLE_TRACE_FOR_CONTROL_GUID__GUID"></span>未能为控件 GUID 启用跟踪： *guid*

通常，当多个跟踪使用者正在收集事件从单个跟踪提供程序在系统上时，将发生此错误。 若要解决此冲突，显示正在运行的计算机上，并且停止发生冲突的会话的所有跟踪会话。

若要显示所有跟踪会话的计算机上，在命令提示符窗口中，键入**traceview-l**。 （TraceView 窗口显示在 TraceView 中运行的跟踪会话。）生成的显示列出了活动的会话。

若要停止跟踪会话，在命令提示符窗口中，键入 **traceview-停止 * * * SessionName*。

有关这些命令的详细信息，请参阅[ **TraceView 控制命令**](traceview-control-commands.md)。

### <a name="span-idcannotopenlogfileforreadingspanspan-idcannotopenlogfileforreadingspancannot-open-logfile-for-reading"></a><span id="cannot_open_logfile_for_reading"></span><span id="CANNOT_OPEN_LOGFILE_FOR_READING"></span>无法打开日志文件进行读取

当你尝试为提供实时跟踪会话或另一个现有跟踪的事件日志中 TraceView 跟踪提供程序显示现有的跟踪日志时，将发生此错误。

### <a name="span-idcannotconnecttoanytracesessioninthegroupspanspan-idcannotconnecttoanytracesessioninthegroupspancannot-connect-to-any-trace-session-in-the-group"></a><span id="cannot_connect_to_any_trace_session_in_the_group"></span><span id="CANNOT_CONNECT_TO_ANY_TRACE_SESSION_IN_THE_GROUP"></span>无法连接到组中的任何跟踪会话

若要解决此错误，请查看[限制的分组](limitations-of-grouping.md)主题，包括可以在系统进行分组的跟踪会话。

### <a name="span-idinternalerrorclosetraceerror170spanspan-idinternalerrorclosetraceerror170spaninternal-error-closetrace-error-170"></a><span id="internal_error__closetrace_error_170"></span><span id="INTERNAL_ERROR__CLOSETRACE_ERROR_170"></span>内部错误：CloseTrace 错误 170

当你尝试加入已在进行的 NT 内核记录器跟踪会话时，将发生此错误。 您可以使用 TraceView 创建 NT 内核记录器跟踪会话，但不能加入由工具或以外 TraceView 方法启动的 NT 内核记录器跟踪会话。

有关详细信息，请参阅[加入跟踪会话](joining-a-trace-session.md)并[NT 内核记录器跟踪会话的创建](creating-an-nt-kernel-logger-trace-session.md)。
