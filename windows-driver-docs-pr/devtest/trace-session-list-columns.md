---
title: 跟踪会话列表列
description: 跟踪会话列表列
ms.assetid: 2e9d7636-3cff-459c-827a-719062bb778c
keywords:
- 跟踪会话列表 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3f630ea21461e0bb84e124807440cf434833202
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519459"
---
# <a name="trace-session-list-columns"></a>跟踪会话列表列


中的列[跟踪会话列表](trace-session-list.md)表示跟踪会话和其跟踪提供程序的属性。 可以设置这些属性中的大多数[日志会话参数选项](log-session-parameter-options.md)选项卡**高级日志会话选项**对话框创建跟踪会话时。 有关详细信息中的选项**日志会话参数选项**选项卡上，请参阅[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

以黑色文本显示它们可显示跟踪会话正在运行时可以更改的属性。 仅当停止跟踪会话时可以更改的属性显示为灰色。 不能更改的跟踪日志中跟踪消息的属性。 有关详细信息，请参阅[更改跟踪会话的属性](changing-the-properties-of-a-trace-session.md)。

以下列表描述所有在跟踪会话列表中，包括默认情况下隐藏的列。 若要了解如何显示隐藏的列，请参阅在"隐藏和显示列"[跟踪会话列表功能](trace-session-list-features.md)。

<span id="Group_ID___Session_Name"></span><span id="group_id___session_name"></span><span id="GROUP_ID___SESSION_NAME"></span>**组 ID / 会话名称**  
显示的组 ID 和会话名称。 不能隐藏此列。

**组 ID**是 TraceView 将分配到跟踪会话的标识符。 将跟踪会话组中的跟踪会话时，TraceView 重新分配到组的单个标识符。 值**组 ID**也会出现在每个窗口框架[跟踪消息列表](trace-message-lists.md)有助于其跟踪消息相关联的跟踪会话的会话。

**会话名称**是给跟踪会话创建时分配的名称。 对于跟踪日志，因为跟踪会话的名称不保存在日志中，所以 TraceView 显示默认会话名称。 不能隐藏此列

<span id="State"></span><span id="state"></span><span id="STATE"></span>**State**  
显示跟踪会话的状态。 此列的有效值为正在运行、 现有、 停止、 已停止、 分组、 分组和 UNGROUPING。

<span id="Event_Count"></span><span id="event_count"></span><span id="EVENT_COUNT"></span>**事件计数**  
对于实时跟踪会话，此列显示 TraceView 自会话后，收到已启动的跟踪消息数。 对于跟踪日志，此列在日志中显示跟踪消息的数。

<span id="Lost_Events"></span><span id="lost_events"></span><span id="LOST_EVENTS"></span>**丢失的事件**  
显示已丢失，因为会话启动的事件数。 通常情况下，事件会丢失，因为跟踪会话耗尽了其缓冲区中的空间。

<span id="Buffers_Read"></span><span id="buffers_read"></span><span id="BUFFERS_READ"></span>**缓冲区读取**  
指定从其 TraceView 接收跟踪消息的缓冲区数。 为现有的跟踪日志，此列显示在跟踪会话中使用的缓冲区数。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**标志**  
指定[跟踪标志](trace-flags.md)跟踪提供程序。 跟踪标志确定提供程序生成的跟踪消息。 每个提供程序由独立确定的标志的含义。

如果可以找到 TraceView[跟踪消息控件 (.tmc) 文件](trace-message-control-file.md)提供程序，您可以选择标志和一个级别从列表中显示**跟踪标志和级别选择**对话框。 若要打开此对话框中，单击**设置**的值**标志**或**级别**跟踪会话列表中的列。

<span id="Flush_Time"></span><span id="flush_time"></span><span id="FLUSH_TIME"></span>**刷新时间**  
指定何种频率 （以秒为单位） （发送到跟踪日志或 TraceView 显示） 跟踪会话缓冲区被刷新。 默认值是 1 （第二个）。

除了当缓冲区已满并且停止跟踪会话时自动发生刷新会发生这些强制刷新问题。 为此列中的 0 值表示执行任何强制的刷新。

运行跟踪会话时，可以更改此值。

<span id="Max_Buf"></span><span id="max_buf"></span><span id="MAX_BUF"></span>**最大 Buf**  
指定为跟踪会话分配的缓冲区的最大数目

默认值取决于数目的处理器、 物理内存量和中使用的操作系统。 运行跟踪会话时，可以更改此值。

<span id="Min_Buf"></span><span id="min_buf"></span><span id="MIN_BUF"></span>**最小值 Buf**  
指定最初分配用于存储跟踪消息的缓冲区数。

如果缓冲区已满，直到它达到中指定的值优先获分配更多的缓冲区**最大 Buf**列。 默认值为**Min Buf**由处理器、 物理内存量和中使用的操作系统的数。 运行跟踪会话时，不能更改此值。

<span id="Buf_Size"></span><span id="buf_size"></span><span id="BUF_SIZE"></span>**Buf 大小**  
指定为跟踪会话分配每个缓冲区的大小，以千字节 (KB)。 默认值取决于数目的处理器、 物理内存量和中使用的操作系统。 运行跟踪会话时，不能更改此值。

<span id="Age"></span><span id="age"></span><span id="AGE"></span>**年龄**  
指定之前则释放未使用的跟踪缓冲区保留的时间长度 （以分钟为单位）。 默认值为“15 分钟”。 在中设置此值**衰减时间**字段[日志会话参数选项](log-session-parameter-options.md)选项卡中**高级日志会话选项**对话框。

仅在 Windows 2000 上使用此值。 运行跟踪会话时，不能更改此值。

<span id="Circular"></span><span id="circular"></span><span id="CIRCULAR"></span>**循环**  
指定跟踪缓冲区是循环，并指定每个缓冲区的最大大小 （以 mb 为单位）。

一个循环缓冲区已满时，新的跟踪消息将写入缓冲区，覆盖最旧的跟踪消息的开头。 默认情况下，跟踪缓冲区都是连续的不能采用循环。

运行跟踪会话时，不能更改此值。

<span id="Sequential"></span><span id="sequential"></span><span id="SEQUENTIAL"></span>**顺序**  
指定跟踪缓冲区是连续，并指定每个缓冲区的最大大小 （以 mb 为单位）。

顺序缓冲区已满时，跟踪消息写入到另一个缓冲区，或将会丢失。 默认情况下，跟踪缓冲区是连续的不能采用循环，并且为 200 MB。

运行跟踪会话时，不能更改此值。

<span id="New_File"></span><span id="new_file"></span><span id="NEW_FILE"></span>**新的文件**  
现有日志文件达到指定的值都将创建新的跟踪日志 (.etl)。 值指定每个日志文件的最大大小以兆字节 (MB)。 在中设置此值**启动新的文件后缓冲区大小**字段[日志会话参数选项](log-session-parameter-options.md)选项卡中**高级日志会话选项**对话框。

仅当提供程序在选择了，它生成跟踪日志时，此值才有效[日志跟踪事件数据，以文件选项](basic-trace-session-options.md)上**日志会话选项**页。 此选项不起作用或中的日志上循环缓冲区[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。 在 Windows 2000 上不支持它。

<span id="Global_Seq"></span><span id="global_seq"></span><span id="GLOBAL_SEQ"></span>**全局 Seq**  
生成全局序列号为每个跟踪消息。

全局序列号的计算机上的所有跟踪会话是唯一的。 默认值是**FALSE**。

此参数不支持在 Windows 2000 上，对中的日志不起[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

<span id="Local_Seq"></span><span id="local_seq"></span><span id="LOCAL_SEQ"></span>**本地 Seq**  
生成本地序列号为每个跟踪消息。 默认值是 **，则返回 TRUE**。

本地序列号跟踪会话中是唯一的。

此参数不支持在 Windows 2000 上，对中的日志不起[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>**级别**  
指定[跟踪级别](trace-level.md)跟踪提供程序。 跟踪级别确定提供程序生成的跟踪消息。 级别值的含义取决于独立每个提供程序。 通常情况下，它表示进一步的详细信息。

如果可以找到 TraceView[跟踪消息控件 (.tmc) 文件](trace-message-control-file.md)提供程序，您可以选择标志和一个级别从列表中显示**跟踪标志和级别选择**对话框。 若要打开此对话框中，单击**设置**的值**标志**或**级别**跟踪会话列表中的列。

有关跟踪级别的详细信息，请参阅的说明*EnableLevel*的参数**EnableTrace** Microsoft Windows SDK 文档中的函数。

<span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>**WinDbg**  
重定向跟踪消息，KD 或的 WinDbg 中，取已启用，除了 TraceView 窗口中显示它们。 此选项还设置缓冲区大小为 3KB，WinDbg 的允许的最大大小。 中显示的值**Buf 大小**列将被忽略。

若要在任何调试程序中显示跟踪消息，wmitrace.dll 和 traceprt.dll 必须在主计算机上的调试程序的搜索路径中。 此外，若要使调试器能够找到跟踪来跟踪消息的消息格式化文件，必须使用 **！ wmitrace.searthpath**专用调试器扩展或设置的值 %跟踪\_格式\_搜索\_PATH %环境变量。 WinDbg 和 WMI 跟踪扩展的信息，请参阅有关 Windows 调试工具。

<span id="Ignore_Traceview"></span><span id="ignore_traceview"></span><span id="IGNORE_TRACEVIEW"></span>**忽略 Traceview**  
取消与 TraceView 操作相关的跟踪消息。

<span id="Max_Trace_Records"></span><span id="max_trace_records"></span><span id="MAX_TRACE_RECORDS"></span>**最大跟踪记录**  
指示跟踪消息的最大数目来 TraceView 存储，然后再开始覆盖最早的邮件以留出空间的较新的消息。

值为**0**意味着没有最大值和 TraceView 保留所有消息，并且永远不会覆盖它们。 默认值是**65536**，对于大多数系统建议的值。 较大的值可能会导致严重延迟。

在中设置此值**虚拟文件大小**字段[日志会话参数选项](log-session-parameter-options.md)选项卡中**高级日志会话选项**对话框。

<span id="Log_File_Name"></span><span id="log_file_name"></span><span id="LOG_FILE_NAME"></span>**日志文件名称**  
显示名称和事件跟踪日志 (.etl) 文件的位置。 实时跟踪会话，此列显示跟踪消息写入到跟踪日志的名称。 对于现有的日志文件，它显示正在从中读取消息的跟踪日志的名称。

<span id="Save_As_Default"></span><span id="save_as_default"></span><span id="SAVE_AS_DEFAULT"></span>**将另存为默认值**  
此选项不是列名称。 它是一个将当前显示的列配置为默认值保存为未来的跟踪会话的命令。 有关详细信息，请参阅 》 中"保存列配置"[跟踪会话列表功能](trace-session-list-features.md)。

 

 





