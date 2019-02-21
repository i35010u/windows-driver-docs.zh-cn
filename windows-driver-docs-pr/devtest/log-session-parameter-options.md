---
title: 日志会话参数选项
description: 日志会话参数选项
ms.assetid: 5398dfa7-abeb-443b-ab64-73b6599c8e73
keywords:
- 跟踪会话 WDK，高级选项
- 跟踪会话 WDK，日志会话参数选项
- 记录会话参数选项 WDK
- 跟踪标志 WDK
- 标志 WDK 软件跟踪
- 刷新时间 WDK 软件跟踪
- 缓冲区 WDK 软件跟踪
- decay 时间 WDK 软件跟踪
- 循环缓冲区 WDK 软件跟踪
- 全局序列号 WDK 软件跟踪
- 跟踪级别 WDK
- 级别 WDK 软件跟踪
- WinDbg WDK 软件跟踪
- 虚拟文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ac2e3012702dc3124420f1b0b32e33a44052c35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540646"
---
# <a name="log-session-parameter-options"></a>日志会话参数选项


在中**日志会话参数选项**选项卡上，可以指定跟踪会话的可变功能的值。

可以设置并创建跟踪会话时更改以下选项中的值。 跟踪会话正在运行时，可以更改多个选项。 不能更改的选项显示为灰色 （"灰显"） 在**日志会话参数选项**对话框。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**标志**  
指定[跟踪标志](trace-flags.md)跟踪提供程序。 跟踪标志确定提供程序生成的跟踪消息。 每个提供程序由独立确定的标志的含义。

如果可以找到 TraceView[跟踪消息控件 (.tmc) 文件](trace-message-control-file.md)提供程序，您可以选择标志和一个级别从列表中显示**跟踪标志和级别选择**对话框。 若要打开**跟踪标志和级别选择**对话框中，单击**设置**的值**标志**或**级别**中选项**日志会话参数选项**对话框。

<span id="Flush_Time__S_"></span><span id="flush_time__s_"></span><span id="FLUSH_TIME__S_"></span>**刷新时间 （秒）**  
指定何种频率 （以秒为单位） 跟踪会话缓冲区刷新到跟踪日志或 TraceView 显示。 默认值是 1 （第二个）。

除了会自动发生缓冲区已满时刷新会发生这些强制刷新问题。 值为 0 表示没有强制的刷新。

若要刷新频率高于每秒一次，请使用**缓冲区大小**可以降低每个缓冲区的大小。

您可以更改**刷新时间**值跟踪会话正在运行时。

<span id="Maximum_Buffers"></span><span id="maximum_buffers"></span><span id="MAXIMUM_BUFFERS"></span>**最大缓冲区**  
指定为跟踪会话分配的缓冲区的最大数目。

默认值取决于数目的处理器、 物理内存量和正在使用的操作系统。 运行跟踪会话时，可以更改此值。

<span id="Minimum_Buffers"></span><span id="minimum_buffers"></span><span id="MINIMUM_BUFFERS"></span>**最小缓冲区**  
指定最初分配用于存储跟踪消息的缓冲区数。

如果缓冲区已满，直到缓冲区的数目达到中指定的值优先获分配更多的缓冲区**最大缓冲区**选项。 默认值取决于数目的处理器、 物理内存量和中使用的操作系统。 运行跟踪会话时，不能更改此值。

<span id="Buffer_Size"></span><span id="buffer_size"></span><span id="BUFFER_SIZE"></span>**缓冲区大小**  
指定为跟踪会话分配每个缓冲区的大小，以千字节 (KB)。 默认值取决于数目的处理器、 物理内存量和中使用的操作系统。 运行跟踪会话时，不能更改此值。

<span id="Decay_Time__Minutes_"></span><span id="decay_time__minutes_"></span><span id="DECAY_TIME__MINUTES_"></span>**Decay 时间 （分钟）**  
指定之前则释放未使用的跟踪缓冲区保留的时间长度 （以分钟为单位）。 默认值为 15。 此选项的值显示在**年龄**的列[跟踪会话列表](trace-session-list.md)。

此参数是仅在 Windows 2000 上有效。 运行跟踪会话时，不能更改此值。

<span id="Circular_Buffer_Size__MB_"></span><span id="circular_buffer_size__mb_"></span><span id="CIRCULAR_BUFFER_SIZE__MB_"></span>**循环缓冲区大小 (MB)**  
指定跟踪缓冲区是循环，并指定每个缓冲区的最大大小 （以 mb 为单位）。

一个循环缓冲区已满时，新的跟踪消息写入缓冲区，覆盖最旧的跟踪消息的开头。 默认情况下，跟踪缓冲区都是连续的不能采用循环。

运行跟踪会话时，不能更改此值。

<span id="Sequential_Buffer_Size__MB_"></span><span id="sequential_buffer_size__mb_"></span><span id="SEQUENTIAL_BUFFER_SIZE__MB_"></span>**顺序缓冲区大小 (MB)**  
指定是否跟踪缓冲区是按顺序，并指定每个缓冲区的最大大小 （以 mb 为单位）。

顺序缓冲区已满时，跟踪消息写入到另一个缓冲区，或将会丢失。 默认情况下，跟踪缓冲区是连续的不能采用循环，并且为 200 MB。

运行跟踪会话时，不能更改此值。

<span id="Start_New_File_After_Buffer_Size__MB_"></span><span id="start_new_file_after_buffer_size__mb_"></span><span id="START_NEW_FILE_AFTER_BUFFER_SIZE__MB_"></span>**缓冲区大小 (MB) 后启动新的文件**  
每当在现有的日志达到指定的值，请创建新的跟踪日志文件 (.etl)。 值以 mb 为单位指定每个日志文件的最大大小。

此选项的值显示在**新的文件**的列[跟踪会话列表](trace-session-list.md)。

仅当提供程序在选择了，它生成跟踪日志时，此选项才有效[日志跟踪事件数据，以文件选项](basic-trace-session-options.md)上**日志会话选项**页。 此选项不起作用或中的日志上循环缓冲区[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。 在 Windows 2000 上不支持它。

<span id="Use_Global_Sequence_Numbers"></span><span id="use_global_sequence_numbers"></span><span id="USE_GLOBAL_SEQUENCE_NUMBERS"></span>**使用全局序列号**  
生成全局序列号为每个跟踪消息。

全局序列号的计算机上的所有跟踪会话是唯一的。 此选项的默认值是**FALSE**。

Windows 2000 中不支持此选项，并对中的日志不起[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

<span id="Use_Local_Sequence_Number"></span><span id="use_local_sequence_number"></span><span id="USE_LOCAL_SEQUENCE_NUMBER"></span>**使用本地的序列号**  
生成本地序列号为每个跟踪消息。 默认值是 **，则返回 TRUE**。

本地序列号跟踪会话中是唯一的。

Windows 2000 中不支持此选项，并对中的日志不起[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>**级别**  
指定[跟踪级别](trace-level.md)跟踪提供程序。 跟踪级别确定提供程序生成的跟踪消息。 级别值的含义取决于独立每个提供程序。 通常情况下，它表示进一步的详细信息。

如果可以找到 TraceView[跟踪消息控件 (.tmc) 文件](trace-message-control-file.md)提供程序，您可以选择标志和一个级别从列表中显示**跟踪标志和级别选择**对话框。 若要打开**跟踪标志和级别选择**对话框中，单击**设置**的值**标志**或**级别**中选项**日志会话参数选项**对话框。

有关跟踪级别的详细信息，请参阅的说明*EnableLevel*的参数**EnableTrace** Microsoft Windows SDK 中的函数。

<span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>**WinDbg**  
重定向跟踪消息，KD 或的 WinDbg 中，取已启用，除了 TraceView 窗口中显示它们。 此选项还设置缓冲区大小为 3KB，WinDbg 的允许的最大大小。 为显示的值**缓冲区大小**选项将被忽略。

若要在调试器中显示跟踪消息，wmitrace.dll 和 traceprt.dll 必须在主计算机上的调试程序的搜索路径中。 中包含这些 Dll[有关 Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=8708)此外，若要使调试器能够找到[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)跟踪消息，TMF 文件必须包含在调试器的搜索在主计算机上的路径。 若要设置的调试程序的搜索路径，请使用 ！ wmitrace.searchpath 专用调试器扩展，或设置的值 %跟踪\_格式\_搜索\_PATH %环境变量。 WinDbg 和 WMI 跟踪扩展的信息，请参阅有关 Windows 调试工具。

<span id="Ignore_TraceView"></span><span id="ignore_traceview"></span><span id="IGNORE_TRACEVIEW"></span>**忽略 TraceView**  
禁止显示生成的 TraceView 操作的跟踪消息。

<span id="Virtual_File_Size"></span><span id="virtual_file_size"></span><span id="VIRTUAL_FILE_SIZE"></span>**虚拟文件大小**  
指示跟踪消息的最大数目来 TraceView 存储，然后再开始覆盖最早的邮件以留出空间的较新的消息。

值为**0**意味着不存在最大值。 TraceView 保留的所有消息并永远不会覆盖它们。 此选项的默认值**65536**，对于大多数系统建议的值。 较大的值可能会导致严重延迟。

此值显示在**最大跟踪记录**的列[跟踪会话列表](trace-session-list.md)。

 

 





