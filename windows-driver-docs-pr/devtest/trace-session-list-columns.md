---
title: 跟踪会话列表列
description: 跟踪会话列表列
keywords:
- 跟踪会话列表 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4a87cba8ae4fe747fb05371223ee2e3171c6841
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816913"
---
# <a name="trace-session-list-columns"></a>跟踪会话列表列


" [跟踪会话" 列表](trace-session-list.md) 中的列表示跟踪会话及其跟踪提供程序的属性。 您可以在创建跟踪会话时，在 "**高级日志会话选项**" 对话框的 "[日志会话参数选项](log-session-parameter-options.md)" 选项卡中设置这些属性。 有关 " **日志会话参数选项** " 选项卡中选项的详细信息，请参阅 [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

运行跟踪会话时可以更改的属性将以黑色文本显示，以显示它们可用。 只有在跟踪会话停止时才可以更改的属性显示为灰色。 无法更改跟踪日志中跟踪消息的属性。 有关详细信息，请参阅 [更改跟踪会话的属性](changing-the-properties-of-a-trace-session.md)。

以下列表描述了 "跟踪会话" 列表中的所有列，包括默认情况下隐藏的列。 若要了解如何显示隐藏的列，请参阅 [跟踪会话列表功能](trace-session-list-features.md)中的 "隐藏和显示列"。

<span id="Group_ID___Session_Name"></span><span id="group_id___session_name"></span><span id="GROUP_ID___SESSION_NAME"></span>**组 ID/会话名称**  
显示组 ID 和会话名称。 不能隐藏此列。

**组 ID** 是 TraceView 分配给跟踪会话的标识符。 在跟踪会话组中组合跟踪会话时，TraceView 会将单个标识符重新分配给组。 **组 ID** 的值还出现在会话的每个 [跟踪消息列表](trace-message-lists.md)的窗口框架中，以帮助你将跟踪会话与跟踪消息相关联。

**会话名称** 是创建跟踪会话时分配给它的名称。 对于跟踪日志，因为跟踪会话的名称未保存在日志中，TraceView 将显示默认的会话名称。 不能隐藏此列

<span id="State"></span><span id="state"></span><span id="STATE"></span>**状态**  
显示跟踪会话的状态。 此列的有效值为正在运行、现有、正在停止、已停止、分组、分组和取消分组。

<span id="Event_Count"></span><span id="event_count"></span><span id="EVENT_COUNT"></span>**事件计数**  
对于实时跟踪会话，此列显示自会话启动后 TraceView 收到的跟踪消息的数量。 对于跟踪日志，此列显示日志中跟踪消息的数量。

<span id="Lost_Events"></span><span id="lost_events"></span><span id="LOST_EVENTS"></span>**丢失的事件**  
显示自会话启动之后丢失的事件数。 通常，事件会丢失，因为跟踪会话在其缓冲区中用尽了空间。

<span id="Buffers_Read"></span><span id="buffers_read"></span><span id="BUFFERS_READ"></span>**缓冲区读取**  
指定 TraceView 从其接收跟踪消息的缓冲区数。 对于现有的跟踪日志，此列显示在跟踪会话中使用的缓冲区数。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定跟踪提供程序的 [跟踪标志](trace-flags.md) 。 跟踪标志确定提供程序生成的跟踪消息。 标志的含义由每个提供程序单独确定。

如果 TraceView 可以找到) 提供程序的 [跟踪消息控制 (](trace-message-control-file.md) ，则可以从 " **跟踪标志和级别选择** " 对话框中显示的列表中选择 "标志" 和 "级别"。 若要打开此对话框，请在 "跟踪会话" 列表中单击 "**标志**" 或 "**级别**" 列的 **设置** 值。

<span id="Flush_Time"></span><span id="flush_time"></span><span id="FLUSH_TIME"></span>**刷新时间**  
指定 (发送到跟踪日志或 TraceView 显示) 刷新跟踪会话缓冲区)  (的频率（以秒为单位）。 默认值为 1 (第二个) 。

除了在缓冲区已满时和跟踪会话停止时自动执行的刷新，还会发生这些强制刷新。 此列中的值为0指示不执行任何强制刷新。

可以在运行跟踪会话时更改此值。

<span id="Max_Buf"></span><span id="max_buf"></span><span id="MAX_BUF"></span>**最大 Buf**  
指定为跟踪会话分配的最大缓冲区数

默认值由处理器数量、物理内存量和使用中的操作系统决定。 可以在运行跟踪会话时更改此值。

<span id="Min_Buf"></span><span id="min_buf"></span><span id="MIN_BUF"></span>**最小 Buf**  
指定最初为存储跟踪消息分配的缓冲区数。

当缓冲区已满时，将分配更多的缓冲区，直到它达到 **Max Buf** 列中指定的值。 **最小 Buf** 的默认值由处理器数量、物理内存量和使用中的操作系统确定。 当跟踪会话正在运行时，不能更改此值。

<span id="Buf_Size"></span><span id="buf_size"></span><span id="BUF_SIZE"></span>**Buf 大小**  
指定分配给跟踪会话的每个缓冲区的大小，以 kb 为单位 (KB) 。 默认值由处理器数量、物理内存量和使用中的操作系统决定。 当跟踪会话正在运行时，不能更改此值。

<span id="Age"></span><span id="age"></span><span id="AGE"></span>**年**  
指定在释放未使用的跟踪缓冲区之前， (用多长时间) 。 默认值为 15 分钟。 此值是在 "**高级日志会话选项**" 对话框的 "[日志会话参数选项](log-session-parameter-options.md)" 选项卡的 "**衰减时间**" 字段中设置的。

此值仅在 Windows 2000 上使用。 当跟踪会话正在运行时，不能更改此值。

<span id="Circular"></span><span id="circular"></span><span id="CIRCULAR"></span>**环状**  
指定跟踪缓冲区为循环，并指定每个缓冲区的最大大小 (（以) MB 为单位）。

当循环缓冲区已满时，会将新的跟踪消息写入缓冲区的开头，并覆盖最早的跟踪消息。 默认情况下，跟踪缓冲区是连续的，而不是循环的。

当跟踪会话正在运行时，不能更改此值。

<span id="Sequential"></span><span id="sequential"></span><span id="SEQUENTIAL"></span>**连续性**  
指定跟踪缓冲区是连续的，并指定每个缓冲区的最大大小 (（以) MB 为单位）。

当顺序缓冲区已满时，跟踪消息将写入另一个缓冲区或丢失。 默认情况下，跟踪缓冲区是连续的，不是循环的，每个都是 200 MB。

当跟踪会话正在运行时，不能更改此值。

<span id="New_File"></span><span id="new_file"></span><span id="NEW_FILE"></span>**新建文件**  
每当现有日志达到指定的值时) 创建新的跟踪日志 (。 该值指定每个日志文件的最大大小（mb） (MB) 。 此值在 "**高级日志会话选项**" 对话框中的 "[日志会话参数选项](log-session-parameter-options.md)" 选项卡的 "**缓冲区大小之后启动新文件**" 字段中设置。

仅当提供程序生成跟踪日志时，此值才有效，也就是说，在 "**日志会话选项**" 页面上选择了 "[日志跟踪事件数据到文件" 选项](basic-trace-session-options.md)。 此选项对来自 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)的循环缓冲区或日志不起作用。 Windows 2000 不支持此方法。

<span id="Global_Seq"></span><span id="global_seq"></span><span id="GLOBAL_SEQ"></span>**全局 Seq**  
为每个跟踪消息生成全局序列号。

全局序列号对于计算机上的所有跟踪会话都是唯一的。 默认值为 **FALSE**。

此参数在 Windows 2000 上不受支持，不会影响 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)中的日志。

<span id="Local_Seq"></span><span id="local_seq"></span><span id="LOCAL_SEQ"></span>**本地 Seq**  
为每个跟踪消息生成本地序列号。 默认值为 **TRUE**。

本地序列号在跟踪会话中是唯一的。

此参数在 Windows 2000 上不受支持，不会影响 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)中的日志。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>**调配**  
指定跟踪提供程序的 [跟踪级别](trace-level.md) 。 跟踪级别确定提供程序生成的跟踪消息。 级别值的含义由每个提供程序单独确定。 通常，它表示详细的详细信息级别。

如果 TraceView 可以找到) 提供程序的 [跟踪消息控制 (](trace-message-control-file.md) ，则可以从 " **跟踪标志和级别选择** " 对话框中显示的列表中选择 "标志" 和 "级别"。 若要打开此对话框，请在 "跟踪会话" 列表中单击 "**标志**" 或 "**级别**" 列的 **设置** 值。

有关跟踪级别的详细信息，请参阅 Microsoft Windows SDK 文档中的 **EnableTrace** 函数的 *EnableLevel* 参数说明。

<span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>**WinDbg**  
除了在 TraceView 窗口中显示跟踪消息以外，还将跟踪消息重定向到 KD 或 WinDbg。 此选项还会将缓冲区大小设置为 3 KB，即 WinDbg 允许的最大大小。 **Buf Size** 列中显示的值将被忽略。

若要在任何调试器中显示跟踪消息，wmitrace.dll 和 traceprt.dll 必须在主计算机上的调试器搜索路径中。 此外，若要使调试器能够查找跟踪消息的跟踪消息格式文件，必须使用 **！ searthpath** 专用调试程序扩展或设置% trace \_ format \_ SEARCH \_ PATH% 环境变量的值。 有关 WinDbg 和 WMI 跟踪扩展的信息，请参阅 Windows 调试工具。

<span id="Ignore_Traceview"></span><span id="ignore_traceview"></span><span id="IGNORE_TRACEVIEW"></span>**忽略 Traceview**  
取消与 TraceView 操作相关的跟踪消息。

<span id="Max_Trace_Records"></span><span id="max_trace_records"></span><span id="MAX_TRACE_RECORDS"></span>**最大跟踪记录**  
指示 TraceView 在开始覆盖最旧的消息之前存储的跟踪消息的最大数目，以便为较新的消息腾出空间。

如果值为 **0** ，则表示没有最大值并且 TraceView 保留所有消息，并且永远不会覆盖它们。 默认值为 **65536**，这是为大多数系统建议的值。 较大的值可能导致明显的延迟。

此值是在 "**高级日志会话选项**" 对话框的 "[日志会话参数选项](log-session-parameter-options.md)" 选项卡的 "**虚拟文件大小**" 字段中设置的。

<span id="Log_File_Name"></span><span id="log_file_name"></span><span id="LOG_FILE_NAME"></span>**日志文件名**  
显示事件跟踪日志 ( .etl) 文件的名称和位置。 对于实时跟踪会话，此列显示跟踪消息写入到的跟踪日志的名称。 对于现有的日志文件，它会显示从中读取消息的跟踪日志的名称。

<span id="Save_As_Default"></span><span id="save_as_default"></span><span id="SAVE_AS_DEFAULT"></span>**另存为默认值**  
此选项不是列名称。 它是一个命令，用于将当前显示的列配置保存为将来跟踪会话的默认配置。 有关详细信息，请参阅 [跟踪会话列表功能](trace-session-list-features.md)中的 "保存列配置"。

 

 





